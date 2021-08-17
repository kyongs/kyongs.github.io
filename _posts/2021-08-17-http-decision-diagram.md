---
layout: post
title: HTTP decision diagram
subheading: HTTP response sequence diagram
author: kyong
categories: Back
tags: API 회사
sidebar: []
---

### 시퀀스 다이어그램 참고 (직접 생각한거라 틀릴 수 있음)

#### Create

``` mermaid!
sequenceDiagram
    UI->>+Devices: POST /sites/{siteId}/devices
    Devices->>+Auth: Token
    alt 토큰이 유효하지 않음
        Auth-->>Devices: 401
        Devices-->>UI: 401 (Unauthorized)
    else 권한 없음
        Auth-->>Devices: 403
        Devices-->>UI: 403 (Forbidden)
    else 정상
        Auth-->>-Devices: 200
        Devices->>Devices: 
        alt 잘못된 요청
            Devices-->>UI: 400(Bad Request)
        else 정상
            Devices->>+DB: DB에 추가
            alt DB FK error
                DB-->>Devices: 
                Devices-->>UI: 400(Bad Request)
            else ID(PK) 이미 존재
                DB-->>Devices: 
                Devices-->>UI: 409(Conflict)
            else 그 외 DB 에러
                DB-->>Devices: 
                Devices-->>UI: 500(Internal Server Error)
            else 정상
                DB-->>-Devices: 
                Devices-->>-UI: 200 (OK)
            end
        end
    end
```


#### Get List

```mermaid!
sequenceDiagram
    UI->>+Devices: GET /sites/{siteId}/devices
    Devices->>+Auth: Token
    alt 토큰이 유효하지 않음
        Auth-->>Devices: 401
        Devices-->>UI: 401 (Unauthorized)
    else 권한 없음
        Auth-->>Devices: 403
        Devices-->>UI: 403 (Forbidden)
    else 정상
        Auth-->>-Devices: 200
        Devices->>Devices: 
        alt 잘못된 요청
            Devices-->>UI: 400(Bad Request)
        else 정상
            Devices->>+DB: DB에 요청
            alt FK 찾지 못함
                DB-->>Devices: 
                Devices-->>UI: 404(Not Found)
            else 그 외 DB 에러
                DB-->>Devices: 
                Devices-->>UI: 500(Internal Server Error)
            else 정상
                DB-->>-Devices: 
                Devices-->>-UI: 200 (OK)
            end
        end
    end
```

#### Get Specific Information

```mermaid!
sequenceDiagram
    UI->>+Devices: GET /sites/{siteId}/devices/{devId}
    Devices->>+Auth: Token
    alt 토큰이 유효하지 않음
        Auth-->>Devices: 401
        Devices-->>UI: 401 (Unauthorized)
    else 권한 없음
        Auth-->>Devices: 403
        Devices-->>UI: 403 (Forbidden)
    else 정상
        Auth-->>-Devices: 200
        Devices->>Devices: 
        alt 잘못된 요청
            Devices-->>UI: 400(Bad Request)
        else 정상
            Devices->>+DB: DB에 요청
            alt FK 찾지 못함
                DB-->>Devices: 
                Devices-->>UI: 404(Not Found)
            else 그 외 DB 에러
                DB-->>Devices: 
                Devices-->>UI: 500(Internal Server Error)
            else 정상
                DB-->>-Devices: 
                Devices-->>-UI: 200 (OK)
            end
        end
    end
```

#### Edit 

```mermaid!
sequenceDiagram
    UI->>+Devices: PUT /sites/{siteId}/devices/{devId}
    Devices->>+Auth: Token
    alt 토큰이 유효하지 않음
        Auth-->>Devices: 401
        Devices-->>UI: 401 (Unauthorized)
    else 권한 없음
        Auth-->>Devices: 403
        Devices-->>UI: 403 (Forbidden)
    else 정상
        Auth-->>-Devices: 200
        Devices->>Devices: 
        alt 잘못된 요청
            Devices-->>UI: 400(Bad Request)
        else 정상
            Devices->>+DB: DB에 수정 요청
            alt FK 찾지 못함
                DB-->>Devices: 
                Devices-->>UI: 404(Not Found)
            else 그 외 DB 에러
                DB-->>Devices: 
                Devices-->>UI: 500(Internal Server Error)
            else 정상
                DB-->>-Devices: 
                Devices-->>-UI: 200 (OK)
            end
        end
    end
```

#### Delete

```mermaid!
sequenceDiagram
    UI->>+Devices: DELETE /sites/{siteId}/devices/{devId}
    Devices->>+Auth: Token
    alt 토큰이 유효하지 않음
        Auth-->>Devices: 401
        Devices-->>UI: 401 (Unauthorized)
    else 권한 없음
        Auth-->>Devices: 403
        Devices-->>UI: 403 (Forbidden)
    else 정상
        Auth-->>-Devices: 200
        Devices->>Devices: 
        alt 잘못된 요청
            Devices-->>UI: 400(Bad Request)
        else 정상
            Devices->>+DB: DB에 삭제 요청
            alt FK error
                DB-->>Devices: 
                Devices-->>UI: 400(Bad Request)
            else 그 외 DB 에러
                DB-->>Devices: 
                Devices-->>UI: 500(Internal Server Error)
            else 정상
                DB-->>-Devices: 
                Devices-->>-UI: 200 (OK)
            end
        end
    end
```


### 이슈 (생각해야하는 시나리오)

1. 추가하려 하는데 DB에 이미 PK가 존재한다

    - 409 conflict error

<br/>

2. 추가하려 하는데 이미 삭제된 상태이다.(조회 api를 날리면 404가 떨어지는 상태)

    - 어떻게 해야할지 - 409는 쓰면 안됨(의미가 다른데 같은 에러 떨구면 안된다)

<br/>


3. 삭제된 상태인데 다시 이전 정보를 살리고 싶다.

    - UPDATE로 Delete Status F로 바꾸면 됨