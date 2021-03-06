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

## 3. Jena 라이브러리 생성

Window - Preferences

![8.png](/assets/img/2019-08-11-1/8.png)

Java - Build Path - User Libraries

![9.png](/assets/img/2019-08-11-1/9.png)

New - Library name 입력 후 OK

![10.png](/assets/img/2019-08-11-1/10.png)

Add External JARs - lib 폴더 안의 모든 파일 열기

![11.png](/assets/img/2019-08-11-1/11.png)

jena-arq-2.9.1.jar - Source attachment(None) 더블클릭 - External location - External File 후 jena-arq jar 파일 선택

![12.png](/assets/img/2019-08-11-1/12.png)

jena-arq-2.9.1.jar - Javadoc location(None) 더블클릭 - Browse - javadoc-arq 폴더 선택

![13.png](/assets/img/2019-08-11-1/13.png)

jena-core, jena-tdb,  jena-iri도 jena-arq와 같은 방법으로 Source와 Javadoc의 경로를 설정해준 뒤 Apply and Close 버튼을 클릭하면 Jena 라이브러리가 생성된다.

## 4. Project에 라이브러리 Import

프로젝트 우클릭 - Build Path - Add Libraries

![14.png](/assets/img/2019-08-11-1/14.png)

User Library - Jena 라이브러리 check - Finish

![15.png](/assets/img/2019-08-11-1/15.png)

이렇게 하면 프로젝트 폴더에 Jena 라이브러리가 생성된 것을 볼 수 있을 것이다. 이제 Jena를 사용할 준비가 되었다.

## 5. Test Code

RDF/XML format으로 작성된 rdf 파일을 읽어 출력하는 예제이다. 읽어오는 [sample 파일](/assets/img/2019-08-11-1/test.rdf)은 다음과 같다.

```xml
<rdf:RDF
  xmlns:rdf='http://www.w3.org/1999/02/22-rdf-syntax-ns#'
  xmlns:vcard='http://www.w3.org/2001/vcard-rdf/3.0#'
 >
  <rdf:Description rdf:about='http://somewhere/JohnSmith'>
    <vcard:FN>John Smith</vcard:FN>
    <vcard:N rdf:nodeID="A0"/>
  </rdf:Description>
  <rdf:Description rdf:nodeID="A0">
    <vcard:Given>John</vcard:Given>
    <vcard:Family>Smith</vcard:Family>
  </rdf:Description>
</rdf:RDF>
```

test 코드는 다음과 같다.

```java
package jena;

import com.hp.hpl.jena.rdf.model.Model;
import com.hp.hpl.jena.rdf.model.ModelFactory;

public class test {
	
	public static void main(String[] args) {
		
		Model m = ModelFactory.createDefaultModel();
		m.read("file:./test.rdf", "RDF/XML");
		
		m.write(System.out, "RDF/XML");
	}
}
```

코드 실행 시 다음과 같이 출력된다면 Jena 라이브러리가 설치된 것이다.

![16.png](/assets/img/2019-08-11-1/16.png)