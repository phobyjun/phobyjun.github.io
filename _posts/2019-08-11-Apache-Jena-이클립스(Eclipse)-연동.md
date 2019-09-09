---
title: "Apache Jena 이클립스(Eclipse) 연동"
excerpt: "Apache Jena 이클립스(Eclipse) 연동"
tags: [java, eclipse, jena, jenaApi, ApacheJena]
comments: true
---

![1.png](/assets/img/2019-08-11-1/1.png)

아파치 제나(Apache Jena)는 Java용 오픈 소스 시맨틱 웹 프레임워크로, RDF 그래프에서 데이터를 추출하거나 기록하는 API를 제공한다. 그래프는 추상적인 모델로 표현되는데 ,파일, 데이터베이스, URL, 또는 이들의 조합에서 데이터를 공급받는다. SPARQL을 통해 질의할 수 있으며, 다른 시맨틱 웹 프레임워크와는 달리 OWL(Web Ontology Language)을 지원한다.

jena는 apache-jena와 apache-jena-fuseki 두 가지 release를 제공한다. apache-jena는 기본적인 API와 SPARQL 엔진, TDB를 command line tools로 제공하고, apche-jena-fuseki는 Jena SPARQL server를 제공한다.

여기서는 Eclipse와 Jena Api를 연동하는 방법을 설명한다.

- java version: java 11.0.2 2019-01-15 LTS
- eclipse version: 2019-06 (4.12.0)
- jena version: apache-jena-2.7.1

## 1. Java Project 생성

File - New - Other

![2.png](/assets/img/2019-08-11-1/2.png)

Java Project 생성

![3.png](/assets/img/2019-08-11-1/3.png)

Project name 입력 후 Finish

![4.png](/assets/img/2019-08-11-1/4.png)

Project 오른쪽 클릭 후 New - Class

![5.png](/assets/img/2019-08-11-1/5.png)

Name 입력 - public static void main(String[] args) 항목 체크(나중에 알아서 만들어줘도 됨) - Finish

![6.png](/assets/img/2019-08-11-1/6.png)

여기까지 Java Project 생성이 끝났다.

## 2. Apache-Jena 다운로드

Jena는 2.7.1 버전을 사용했다.

2.7.1 버전은 [이곳](http://archive.apache.org/dist/jena/binaries/apache-jena-2.7.1.zip)에서 다운로드 받을 수 있다.

다운로드 받으면 여러 개의 파일들이 존재하지만, 사진 속 빨간 네모 박스 안의 파일들로만 Java 라이브러리를 만들어 사용할 것이다.

![7.png](/assets/img/2019-08-11-1/7.png)

