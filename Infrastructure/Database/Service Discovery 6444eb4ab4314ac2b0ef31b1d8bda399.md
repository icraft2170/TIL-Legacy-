# Service Discovery

대분류: 백엔드
작성여부: No
최종 편집일: 2022년 8월 26일 오전 1:04
키워드: MSA

# 서비스 디스커버리 ( Service Discovery )

> **Service Discovery 란?**
> 

MSA: Micro Service Architecture 에서는 다양한 Micro Service에 상호작용을 통해 작동하고, 이러한 Micro Service 들은 서로 다른 IP와 Port를 가진다. 

서비스들은 서로 원격 호출을 통해 상호작용을 하는데 원격 호출을 위해서는 IP와 Port가 필요하고 때문에 `**Key-Value` 형태로 IP와 Port를 저장및 관리하며 Micro Service간의 상호작용에 도움을 주는 역할을 한다.**

**그 구조만 보면 마치 DNS 와 유사하여, 각 서비스의 위치를 기억하고 찾아준다. Java 진영에서는 대표적으로 Service Discovery 로 `유레카(Eureka)` 를 사용한다.**

![Untitled](Service%20Discovery%206444eb4ab4314ac2b0ef31b1d8bda399/Untitled.png)

### Spring Eureka