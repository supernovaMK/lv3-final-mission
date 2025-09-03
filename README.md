# 인프라 설정
이 프로젝트는 Spring Boot 애플리케이션과 MySQL 데이터베이스를 분리된 환경에서 실행하도록 구성되었습니다.

## 아키텍처 개요
* 애플리케이션: EC2 인스턴스에서 실행 (git clone 후 docker-compose로 배포)
이런 방식으로 설계하였을 경우에는 추후에 docker image를 활용하여 버전 롤백을 편리하게 적용할 수 있고, 하나의 인스턴스에서 두개의 컨테이너를 통해서 무중단 배포를 시도할 수 있습니다.
* 데이터베이스: Docker 기반 MySQL 컨테이너로 실행 (별도 서버에서 배포)
이 방식을 통해서 application서버가 중단되더라도 db 서버는 영향이 없어 데이터가 유실 될 가능성이 적어집니다.
* 연결 방식: Spring Boot → MySQL (JDBC URL 기반)
* 환경변수 관리: .env 파일과 application.properties 조합
이 방식을 사용하여 숨기고 싶은 환경변수들을 감추어 github에 올라가는 코드에서 가릴 수 있습니다. 추후에는 git submodule등을 활용하여 환경변수들을 가릴 수 있을 것 같습니다.
