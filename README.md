# Домашнее задание к занятию "`GitLab`" - `Вялов владислав`


### Задание 1

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 1](ссылка на скриншот 1)`


 скриншот 1 https://disk.yandex.ru/i/za4hDkPWTcXnlw
 
 скриншот 2  https://disk.yandex.ru/i/RBmberTYGb03-Q

 скриншот 3 https://disk.yandex.ru/i/pfykobj7LkRDqw

 скриншот 4 https://disk.yandex.ru/i/AV-MT12N053PSg

### Задание 2

.gitlab-ci.yml
```
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

variables:
  NODE_VERSION: "18"

# Этап 1: Тестирование
unit-tests:
  stage: test
  image: node:$NODE_VERSION
  script:
    - echo "Running unit tests..."
    - npm install
    - npm test
  artifacts:
    when: always
    paths:
      - coverage/
    reports:
      junit: junit.xml
  only:
    - main
    - merge_requests

integration-tests:
  stage: test  
  image: node:$NODE_VERSION
  script:
    - echo "Running integration tests..."
    - npm run integration-test
  dependencies:
    - unit-tests

# Этап 2: Сборка
build:
  stage: build
  image: node:$NODE_VERSION
  script:
    - echo "Building application..."
    - npm run build
    - echo "Build completed successfully!"
  artifacts:
    paths:
      - dist/
      - build/
  only:
    - main

docker-build:
  stage: build
  image: docker:latest
  services:
    - docker:dind
  script:
    - echo "Building Docker image..."
    - docker build -t my-app:latest .
    - docker images
  dependencies:
    - build
  only:
    - main

# Этап 3: Деплой
deploy-staging:
  stage: deploy
  image: alpine:latest
  script:
    - echo "Deploying to staging environment..."
    - apk add --no-cache curl
    - curl -X POST https://api.staging.com/deploy
    - echo "Staging deployment completed!"
  environment:
    name: staging
    url: https://staging.example.com
  only:
    - main

deploy-production:
  stage: deploy
  image: alpine:latest  
  script:
    - echo "Deploying to production..."
    - echo "Production deployment would happen here"
  environment:
    name: production
    url: https://production.example.com
  when: manual
  only:
    - main

# Этапы которые всегда выполняются
code-quality:
  stage: test
  image: node:$NODE_VERSION
  script:
    - echo "Checking code quality..."
    - npm run lint
    - npm run type-check
  allow_failure: true

security-scan:
  stage: test
  image: alpine:latest
  script:
    - echo "Running security scan..."
    - apk add --no-cache git
    - git secrets --scan
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты

 скриншот 1 https://disk.yandex.ru/i/UjHYohRVJQFgLA
 
 скриншот 2  https://disk.yandex.ru/i/eBocJNj-eeB4XQ

 скриншот 3 https://disk.yandex.ru/i/hY2AJN6EMvX3mw

 скриншот 4 https://disk.yandex.ru/i/6s4yE_qHMuB15A


---

