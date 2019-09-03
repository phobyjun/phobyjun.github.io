---
title: "Data Catalog Vocabulary (DCAT)"
excerpt: "Data Catalog Vocabulary (DCAT)"
tags: [Silk, Tech, LOD, DCAT, dcat, schema, rdf]
comments: true
---

## Abstract

DCAT는 Web상에서 만들어진 데이터 catalog들 사이의 정보 처리 상호 운용(interoperability)를 용이하게 하기 위해 고안된 RDF 어휘이다.

DCAT는 표준 모델과 여러 개의 catalog들로부터 나온 메타데이터의 집합과 사용을 용이하게 하는 어휘를 사용한 catalog 안의 데이터 서비스들과 데이터셋들을 publisher로 하여금 묘사할수 있도록 한다. 이는 데이터셋 또는 데이터 서비스들을 더욱 잘 발견할수 있게 한다. 이는 또한 이미 만들어진 데이터 catalog들에 대한 분산된 접근을 가능하게 하며, 여러 개의 사이트에 있는 데이터셋들 간의 catalog들을 동일한 질의(query) 메커니즘과 구조(structure)로 통일된 검색을 가능하게 한다. 수집된 DCAT 메타데이터는 디지털 보존 과정의 한 부분처럼 명백한 파일을 제공할 수 있다.

DCAT tems의 namespace는 다음과 같다:

- [http://www.w3.org/ns/dcat#](http://www.w3.org/ns/dcat#)

DCAT namespace의 prefix는 다음과 같다:

- dcat

## 1. Introduction

서로 다른 조직, 연구자, 정부 그리고 시민들 사이에서 공유된 데이터 리소스들은 메타데이터의 규약을 필요로 한다. 이는 그 데이터가 열려있는지 아닌지를 상관하지 않는다. DCAT는 Web상에 올라가 있는 데이터 catalog들의 어휘인데, 여기서 Web은 [data.gov](https://www.data.gov/)나 [data.gov.uk](https://data.gov.uk/)와 같은 정부 데이터 catalog들의 배경에서 처음부터 개발된 곳이다. 하지만 이는 또한 적용 가능하고 다른 배경들에서 사용되어 왔다.

이 DCAT의 개정판은 use case와 필수인 [DCAT-UCR](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-dcat-ucr)에 더불어 지원하기 위한 이전 버전을 확장했다. 이는 데이터 서비스, 데이터셋들 이외의 다른 자원들을 catalog화 하는 가능성을 포함한다. 이 개정판은 또한 데이터셋들의 관계를 데이터셋과 다른 catalog화된 자원들 사이의 관계만큼 잘 묘사하는 과정을 지원한다. 

DCAT는 catalog 안에서 데이터 서비스들과 데이터셋들이 묘사되고 포함될 수 있게 허락해주는 RDF classes와 properties를 제공한다. 표준 모델과 어휘의 사용은 다양한 catalog들로부터의 메타데이터를 사용하고 모아주는 것을 용이하게 한다. 우리가 할 수 있는 것은 다음과 같다:

1. 데이터셋과 데이터 서비스들을 더욱 잘 발견할 수 있게 한다.
2. 다양한 사이트들에 존재하는 catalog들 사이의 데이터셋들을 위한 federated search를 허락한다.

데이터는 catalog 안에서 스프레드시트(spreadsheets)부터 XML과 RDF를 거쳐 다양한 형식으로 묘사될 수 있다. DCAT는 데이터셋의 serialize된 형식에 관한 가정을 세우지 않는다. 다만 이는 추상 데이터셋과 그것들의 다른 명시 또는 배포 사이에서 구분할 뿐이다.

상호 보완적인 어휘들은 더욱 자세한 형식-구체적(format-specific) 정보를 제공하는 DCAT와 함께 사용될 수 있다. 예를 들어 [VoID](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-void) 어휘의 특성은 만약 데이터셋이 RDF 형식이라면 이에 대한 다양한 통계를 표현하기 위해 DCAT 안에서 사용될 수 있다.

## 2. Motivation for change

[Link](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#motivation)

## 3. Namespaces

DCAT의 namespace는 http://www.w3.org/ns/dcat#이다. 그러나 DCAT는 Dublin Core [DCTERMS](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-dcterms)와 같은 다른 어휘들로부터의 외부 용어를 사용한다. DCAT는 어떠한 데이터셋이 가지고 있는 class와 properties들의 작은 집합을 정의한다.

| Prefix         | Namespace                                        |
| -------------- | ------------------------------------------------ |
| adms           | https://www.w3.org/ns/adms#                      |
| dc             | http://purl.org/dc/elements/1.1/                 |
| dcat           | http://www.w3.org/ns/dcat#                       |
| dct            | http://purl.org/dc/terms/                        |
| dctype         | http://purl.org/dc/dcmitype                      |
| dqv            | http://www.w3.org/ns/dqv#                        |
| earl           | http://www.w3.org/ns/earl#                       |
| foaf           | http://xmlns.com/foaf/0.1/                       |
| geosparql      | http://www.opengis.net/ont/geosparql#            |
| locn           | http://www.w3.org/ns/locn#                       |
| oa             | http://www.w3.org/ns/oa#                         |
| odrl           | http://www.w3.org/TR/odrl-vocab/#                |
| owl            | http://www.w3.org/2002/07/owl#                   |
| prov           | http://www.w3.org/ns/prov#                       |
| rdf            | http://www.w3.org/1999/02/22-rdf-syntax-ns#      |
| rdfs           | http://www.w3.org/2000/01/rdf-schema#            |
| sdmx-attribute | http://purl.org/linked-data/sdmx/2009/attribute# |
| sdo            | https://schema.org/                              |
| skos           | http://www.w3.org/2004/02/skos/core#             |
| time           | http://www.w3.org/2006/time#                     |
| vcard          | http://www.w3.org/2006/vcard/ns#                 |
| w3cgeo         | http://www.w3.org/2003/01/geo/wgs64_pos#         |
| xsd            | http://www.w3.org/2001/XMLSchema#                |

## 4. Conformance(권고 사항)

[Link](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#conformance)

## 5. Vocabulary overview

### 5.1 DCAT scope

DCAT는 데이터 catalog들은 표현하기 위한 RDF 어휘이다. DCAT는 다음 8개의 main class들을 기본으로 한다:

- [dcat:Catalog](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Catalog)는 자원을 묘사하는 메타데이터 record인 각각의 요소들이 있는 데이터셋인 catalog를 표현한다. dcat:Catalog의 범위는 **데이터셋** 또는 **데이터 서비스**에 관한 메타데이터의 모음이다.
- [dcat:Resource](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Resource)는 catalog 안에 있는 각각의 요소를 표현한다. 이 class는 직접적으로 사용되도록 유도되지 않는다. 다만 이는 dcat:Dataset, dcat:DataServies 그리고 dcat:Catalog의 부모 class이다. catalog 안의 멤버 요소는 하위 class, 또는 그것들의 하위 class, 또는 DCAT profile이나 다른 DCAT application에서 정의된 dcat:Resource의 하위 class의 멤버여야 한다. dcat:Resource는 실제로 어떤 종류의 자원이든 catalog를 정의하기 위한 확장된 point이다.
- [dcat:Dataset](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Dataset)는 catalog의 데이터셋을 표현한다. 데이터셋은 단일 agent에 의해 만들어지고(published) 배포된(curated) 데이터의 모음이다. 데이터는 숫자, 단어, 픽셀, 이미지, 소리 그리고 다른 multi-media, 그리고 데이터셋으로 모아질 수 있는 어떤 가능성있는 다른 형태를 포함한 여러 가지 형태로 만들어진다.
- [dcat:Distribution](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Distribution)는 다운로드 가능한 파일과 같은 데이터셋의 접근 가능한 형태를 표현한다.
- [dcat:DataService](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Data_Service)는 catalog의 데이터 서비스를 표현한다. 데이터 서비스는 하나 또는 그 이상의 데이터셋 또는 데이터 처리 기능에 대한 접근을 제공하는 **API**를 통한 접근하기 쉬운 기능의 집합이다.
- [dcat:CatalogRecord](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Catalog_Record)는 catalog 안에서 요소들이 언제 더해지고 누가 더했는지와 같은 registration 정보를 우선적으로 나타내는 catalog 안의 메타데이터 요소를 표현한다.

**Figure 1. Overview of DCAT model, showing the classes of resources that can be members of a Catalog, and the relationship between them.**

![1](/assets/img/2019-07-27-1/1.png)

### 5.2 RDF considerations

DCAT 어휘는 [RDF-SCHEMA](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-rdf-schema)를 사용해 형식화된 OWL2 ontology [OWL2 ontology](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-owl2-overview) 이다. DCAT의 각각의 class와 property는 [IRI](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-iri)에 의의 표시되었다. 지역적으로(locally) 정의된 요소들은 namespace (http://www.w3.org/ns/dcat#)에 있다. 요소들은 또한 몇몇 [FOAF](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-foaf), [DCTERMS](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-dcterms)와 [PROV-O](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-prov-o)와 같은 외부 어휘들로부터 가져왔다.

### 5.3 Basic example

이 예제는 DCAT가 정부 catalog와 그것들의 데이터셋들은 표현하는 데에 어떻게 사용되는지에 대한 quick overview를 제공한다.

첫번째로, catalog description이다:

> EXAMPLE 1
>
> ```xml
> :catalog
> 	a dcat:Catalog ;
> 	dct:title "Imaginary Catalog" ;
> 	rdfs:label "Imaginary Catalog" ;
> 	foaf:homepage <http://example.org/catalog> ;
> 	dct:publisher :transparency-office ;
> 	dct:language <http://id.loc.gov/vocabulary/iso639-1/en> ;
> 	dct:dataset :dataset-001 , :dataset-001 , :dataset-003 ;
> 	.
> ```

catalog의 publisher는 relative URI인 :transparency-office를 가진다. publisher에 대한 묘사는 다음 예제와 같이 제공될 수 있다:

> EXAMPLE 2
>
> ```xml
> :transparency-office
> 	a foat:Organization ;
> 	rdfs:label "Transparency Office" ;
> 	.
> ```

catalog는 dcat:dataset 특성을 통해 각각의 dataset들을 나열한다. EXAMPLE 1에서, 예제 데이터셋은 relative URI :dataset-001을 나타낸다. DCAT를 이용한 가능한 description은 다음과 같다:

> EXAMPLE 3
>
> ```
> :dataset-001
> 	a dcat:Dataset ;
> 	dct:title "Imaginary dataset" ;
> 	dcat:keyword "accountability", "transparency", "payments" ;
> 	dct:creator :finance-employee-001 ;
> 	dct:issued "2011-12-05"^^xsd:date ;
> 	dct:modified "2011-12-15"^^xsd:date ;
> 	dcat:contactPoint <http://example.org/transparency-offic/contact> ;
> 	dct:temporal <http://reference.data.gov.uk/id/quarter/2006-Q1> ;
> 	dcat:temporalResolution "P1D"^^xsd:duration ;
> 	dct:spatial <http://www.geonames.org/6695072> ;
> 	dcat:spatialResolutionInMeters "30.0"^^xsd:decimal ;
> 	dct:publisher :finance-ministry ;
> 	dct:language <http://id.loc.gov/vocabulary/iso639-1/en> ;
> 	dct:accrualPeriodicity <http://purl.org/linked-data/sdmx/2009/code#freq-W> ;
> 	dcat:distribution :dataset-001-csv ;
> ```

다섯 개의 구분된 temporal 기술자는 이 데이터셋을 보여준다. 데이터셋 publication과 revision 날짜는 dct:issued과 dct:modified에서 보여준다. dct:accuralPeriodicity의 데이터셋의 업데이트 횟수를 위해, 우리는 W3C Data Cube Vocabulary의 한 부분으로 개발된 [content-oriented-guidelines](https://www.w3.org/TR/vocab-data-cube/#dsd-cog)로부터의 instance를 사용한다.  temporal coverage 또는 extent는 data.gov.uk의 interval 데이터셋으로부터의 요소를 사용한 dct:temporal로 주어진다(원칙적으로는 http://reference.data.gov.uk/id/inteval에서 사용 가능하다). 데이터셋 안 요소의 minimun spacing을 나타내는 temporal resolution은 표준 데이터 형식인 xsd:duration을 사용한 dcat:temporalResolution으로 주어진다.

추가적으로, 지역의 범위 또는 넓이는 [Geonames](http://www.geonames.org/)로부터의 URI를 사용한 dct:sparial로 주어진다. 데이터셋 안 요소의 minimum spatial separation을 나타내는 지역 resolution은 표준 데이터 형식은 xsd:decimal을 사용한 dcat:spatialResolutionInMeters로 주어진다.

contact point는 보내질 수 있는 데이터셋에 관한 피드백과 comment들이 있는 곳에서 제공되었다. 이메일 주소나 전화 번호 같은 더 많은 contact point에 관한 정보는 [vCard](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-vcard-rdf)를 사용해 제공될 수 있다.

데이터셋 :dataset-001-csv이 5kb의 CSV 파일로 다운로드 될 수 있는 예제가 있다. 이는 RDF 자원 형식인 dcat:Distribution으로 나타내어진다:

> EXAMPLE 4
>
> ```
> :dataset-001-csv
> 	a dcat:Distribution ;
> 	dcat:downloadURL <http://www.example.org/files/001.csv> ;
> 	dct:title "CSV distribution of imaginary dataset 001" ;
> 	dcat:mediaType <https://www.iana.org/assignments/media-types/test/csv> ;
> 	dcat:byteSize "5120"^^xsd:dscimal ;
> 	.
> ```

## 6. Vocabulary specification

### 6.1 RDF representation

개정판 DCAT 어휘는 [RDF로 사용 가능하다](https://github.com/w3c/dxwg/tree/gh-pages/dcat/rdf/). 첫 번째로 있는 artefact인 dcat.ttl은 핵심 DCAT 어휘의 serialization이다. 그 외의 다른 형식의 RDF 파일들은 추가적인 정보를 제공하는데, 다음과 같다:

1. guidance를 위해 제공된 비표준적인 다른 어휘들의 모음
2. 몇몇 문잭들에서 사용 가능한 추가적인 axiom들
3. 2014년 버전의 DCAT와 일치하는 profile을 포함한 몇몇 DCAT의 profile들 ([VOCAB-DCAT-20140116](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-vocab-dcat-20140116))

이 문서에서는 dcat:dataset에 관한 내용만을 설명할 것이다.

### 6.4 Class: Cataloged Resource

| RDF Class:  | dcat:Resource                                                |
| ----------- | ------------------------------------------------------------ |
| Definition: | 단일 agent에 의해 공표되고 배포된 자원.                      |
| Usage note: | 모든 catalog화된 자원들의 class, dcat:dataset, dcat:DataService, dcat:Catalog 그리고 dcat:Catalog의 다른 멤버들의 super-class. 이 class는 데이터셋과 데이터 서비스들을 포함한 모든 catalog화 된 자원들에게 property들을 전한다. 이것이 사용 가능할 때 더욱 구체적인 sub-class를 사용하는 것이 강력하게 권장된다. |
| Usage note: | dcat:Resource는 어떤 종류의 catalog든지 정의 가능한 extension point이다. 추가적인 sub-class들은 다른 종류의 자원의 catalog를 위한 DCAT profile 또는 DCAT application으로 정의될 수 있다. |

#### 6.4.1 Property: access rights

| RDF Property: | dct:accessRights                                             |
| ------------- | ------------------------------------------------------------ |
| Definition    | 자원이 어떻게 접근되어지는지 고려하는 권리 진술.             |
| Range:        | dct:RightStatement                                           |
| Usage note:   | license와 right들에 관한 정보는 *아마도(MAY)* 자원을 위해 제공된다. 더욱 많은 guidance를 [8. License and rights statements](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#license-rights)에서 확인해라. |

#### 6.4.2 Property: conforms to

| RDF Property: | dct:conformsTo                                               |
| ------------- | ------------------------------------------------------------ |
| Definition    | catalog화된 자원의 conform들을 묘사하기 위한 표준.           |
| Range:        | dct:Standard ("비교를 위한 기초; 평가될 수 있는 다른 것에 반하는 reference point" [DCTERMS](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-dcterms)) |
| Usage note:   | 이 특성은 *무조건(SHOULD)* catalog화된 자원을 conform하는 model, schema, ontology, view 그리고 profile을 확인하는 데에 사용되어야만 한다. |

#### 6.4.3 Property: contact point

| RDF Property: | dcat:contactPoint                                            |
| ------------- | ------------------------------------------------------------ |
| Definition:   | catalog화된 자원을 위한 관련 연락 정보. [VCARD-RDF](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-vcard-rdf)의 사용이 권장됨 |
| Range:        | vcard:kind                                                   |

#### 6.4.4 Property: resource creator

| RDF Property: | dct:creator                                                  |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 자원을 제공한 총 책임자.                                     |
| Range:        | foaf:Agent                                                   |
| Usage note:   | 이 특성을 위한 value들로서 자원 형식인 foaf:Agent가 권장된다. |

#### 6.4.5 Property: description

| RDF Property: | dct:description          |
| ------------- | ------------------------ |
| Definition:   | item을 기록한 free-text. |
| Range:        | rdfs:Literal             |

#### 6.4.6 Property: title

| RDF Property: | dct:title          |
| ------------- | ------------------ |
| Definition:   | item에 주어진 이름 |
| Range:        | rdfs:Literal       |

#### 6.4.7 Property: release date

| RDF Property: | dct:issued                                                   |
| ------------- | ------------------------------------------------------------ |
| Definition:   | item이 공식적으로 발표된 날짜.                               |
| Range:        | 관련된 ISO 8601 Date and Time compliant string ([DATETIME](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-datetime))을 사용해 인코딩된 rdfs:Literal과 적절한 XML Schema datatype ([XMLSCHEMA11-2](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-xmlschema11-2))을 사용한 형식. |
| Usage note:   | 이 특성은 *무조건(SHOULD)* 첫 번째로 알려진 발표 날짜를 사용해 지정되어야 한다. |

#### 6.4.8 Property: update/modification date

| RDF Property: | dct:modified                                                 |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 가장 최근에 item이 바뀌거나 수정되거나 업데이트 된 날짜.     |
| Range:        | 관련된 ISO 8601 Date and Time compliant string ([DATETIME](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-datetime))을 사용해 인코딩된 rdfs:Literal과 적절한 XML Schema datatype ([XMLSCHEMA11-2](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-xmlschema11-2))을 사용한 형식. |
| Usage note:   | 이 특성의 값은 caralog record의 수정이 아닌 실제 item의 수정을 보여준다. 만약 값이 없다면, *아마도(MAY)* 이는 초기 발표 이후 어떠한 수정도 없었다는 것을 의미하거나 마지막으로 수정된 날짜를 알지 못하거나 item이 지속적으로 업데이트 되었다는 것을 의미한다. |

#### 6.4.9 Property: language

| RDF Property: | dct:language                                                 |
| ------------- | ------------------------------------------------------------ |
| Definition:   | item의 언어. 이는 catalog화된 자원의 문자 메타데이터나 데이터셋 분류의 문자 value들을 위해 사용되는 자연어를 가리킨다. |
| Range:        | dct:LinguisticSystem<br />Library of Congress([ISO 639-1](http://id.loc.gov/vocabulary/iso639-1.html), [ISO 639-2](http://id.loc.gov/vocabulary/iso639-2.html))에 의해 정의된 자원들이 *무조건(SHOULD)* 사용되어야 한다.<br />만약 ISO 639-1 코드가 language를 위해 정의되면, 그것과 일치하는 IRI가 *무조건(SHOULD)* 사용되어야 한다. 만약 어떤 ISO 639-1 코드도 사용되지 않는다면, ISO 639-2 코드와 일치하는 IRI가 *무조건(SHOULD)* 사용되어야 한다. |
| Usage note:   | 자원이 2개 이상의 언어로 사용 가능하다면, 이 특성을 반복해서 사용해야 한다. |
| Usage note:   | catalog의 멤버를 위해 제공된 value는 만약 그것들이 충돌될 때에 catalog를 위해 제공된 value를 덮어쓴다. |
| Usage note:   | 만약 데이터셋의 표현이 각각의 언어에서 자별적으로 사용 가능하다면, 각각의 언어를 위한 dcat:Distribution의 instance를 정의하고 dct:language를 사용해 각각의 distribution의 구체적인 언어를 묘사한다. |

#### 6.4.10 Property: publisher

| RDF Property: | dct:publisher                                                |
| ------------- | ------------------------------------------------------------ |
| Definition:   | item을 사용 가능하게 만드는 데에 책임이 있는 entity.         |
| Usage note:   | 이 특성을 위한 value들로서 자원 형식인 foaf:Agent가 권장된다. |

#### 6.4.11 Property: identifier

| RDF Property: | dct:identifier                                               |
| ------------- | ------------------------------------------------------------ |
| Definition:   | item의 유일한 식별자.                                        |
| Range:        | rdfs:Literal                                                 |
| Usage note:   | identifier는 item의 URI의 한 부분으로 사용될 수도 있지만, 여전히 명시적으로 표현하는 것이 유용하다. |

#### 6.4.12 Property: theme/category

| RDF Property:    | dcat:theme                                                   |
| ---------------- | ------------------------------------------------------------ |
| Definition:      | 자원의 main category. 자원은 2개 이상의 theme들을 가질 수 있다. |
| Sub-property of: | dct:subject                                                  |
| Range:           | skos:Concept                                                 |
| Usage note:      | 자원들을 categorize하기 위해 사용된 skos:Concept들은 catalog 안에서 모든 category들과 그것들의 관계를 기술하기 위해 skos:ConceptScheme으로 조직화된다. |

#### 6.4.13 Property: type/genre

| RDF Property:    | dct:type                                                     |
| ---------------- | ------------------------------------------------------------ |
| Definition:      | 자원의 nature 또는 genre                                     |
| Sub-Property of: | dc:type                                                      |
| Range:           | rdfs:Class                                                   |
| Usae note:       | value들은 *무조건(SHOULD)* 잘 관리되고 광범위하게 알려진 controlled vocabulary로부터 가져와야 한다. 예시는 다음과 같다:<br />1. [DCMI Type vocabulary](http://dublincore.org/documents/dcmi-terms/#section-7) [DCTERMS](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-dcterms)<br />2. [ISO-19115-1](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-iso-19115-1) [scope codes](https://geo-ide.noaa.gov/wiki/index.php?title=ISO_19115_and_19115-2_CodeList_Dictionaries#MD_ScopeCode)<br />3. [Datacite resource types](https://schema.datacite.org/meta/kernel-4.1/include/datacite-resourceType-v4.1.xsd) [DataCite](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-datacite)<br />4. PARSE.Insight cotent-types used by [re3data.org](https://www.re3data.org/) [RE3DATA-SCHEMA](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-re3data-schema)<br />5. [MARC intellectual resource types](http://id.loc.gov/vocabulary/marcgt.html)<br />몇몇 이 controlled vocabularies들의 멤버들은 데이터셋이나 데이터서비스들과 정확이 들어맞지는 않는다. 하지만, DCAT profile이나 application들에서 정의된 다른 종류의 catalog의 문맥에서 사용될지도 모른다. |
| Usage note:      | 파일 형식, 물리적 medium, 자원의 dimension들을 기술하기 위해서는, dct:format 요소가 사용된다. |

#### 6.4.14 Property: resource relation

| RDF Property: | dct:relation                                                 |
| ------------- | ------------------------------------------------------------ |
| Definition:   | catalog화된 item과 구체적이지 않은 관계에 있는 자원.         |
| Usage note:   | dct:relation은 *무조건(SHOULD)* catalog화된 item과 관련된 알려지지 않은 자원 사이의 관계의 nature에서 사용되어야 한다. 더욱 구체적인 sub-property는 *무조건(SHOULD)* link의 관계의 nature가 알려져 있을때 사용되어야 한다. 특성 dcat:distribution는 *무조건(SHOULD)* dcat:Distribution으로 기술된 데이터셋의 표현을 위한 dcat:Dataset으로부터의 link로 사용되어야 한다. |

#### 6.4.15 Property: qualified relation

| RDF Property:    | dcat:qualifiedRelation                 |
| ---------------- | -------------------------------------- |
| Definition:      | 다른 자원과의 관계의 묘사를 위한 link. |
| Sub-property of: | prov:qualifiedInfluence                |
| Domain:          | dcat:Resource                          |
| Range:           | dcat:Relationship                      |

#### 6.4.16 Property: keyword/tag

| RDF Property: | dcat:keyword                          |
| ------------- | ------------------------------------- |
| Definition:   | 자원을 묘사하기 위한 keyword 또는 tag |
| Range:        | rdfs:Literal                          |

#### 6.4.17 Property: landing page

| RDF Property:    | dcat:landingPage                                             |
| ---------------- | ------------------------------------------------------------ |
| Definition:      | 웹 브라우저 안에서 catalog, 데이터셋, distribution 그리고(또는) 추가적인 정보에 접근할 수 있도록 안내할 수 있는 웹 페이지. |
| Sub-Property of: | foat:page                                                    |
| Range:           | foaf:Document                                                |
| Usage note:      | 만약 distribution이 오직 landing page를 통해 접근 가능하다면, landing page link는 *무조건(SHOULD)* distribution의 dcat:accessURL과 같다야 한다. |

#### 6.4.18 Property: qualified attribution

| RDF Property:    | prov:qualifiedAttribution                                    |
| ---------------- | ------------------------------------------------------------ |
| Definition:      | 이 자원의 형식에 대한 책임이 있는 Agent의 link               |
| Sub-Property of: | prov:qualifiedInfluence                                      |
| Domain           | prov:Entity                                                  |
| Range            | prov:Attribution                                             |
| Usage note:      | 관계의 nature가 잘 알려져 있지만 표준 특성 중 어느 하나라도 관계가 없는 Agent로의 link를 위해 사용된다. 자원의 관점에서 Agent의 책임을 확인하기 위해 prov:Attribution의 dcat:hadRole을 사용한다. |

#### 6.4.19 Property: license

| RDF Property: | dct:license                                                  |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 자원이 사용 가능하도록 만들어졌는지에 대한 법적인 문서.      |
| Range:        | dct:LicenseDocument                                          |
| Usage note:   | right와 license들에 관한 정보는 *아마도(MAY)* 자원을 위해 제공되어질 것이다. |

#### 6.4.20 Property: rights

| RDF Property: | dct:rights                                                   |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 저작권과 같은 dct:license 또는 dct:accessRights들과 관련이 었는 모든 right들과 관련이 있는 statement. |
| Range:        | dct:RightsStatement                                          |
| Usage note:   | right와 license들에 관한 정보는 *아마도(MAY)* 자원을 위해 제공되어질 것이다. |

#### 6.4.21 Property: has policy

| RDF Property: | odrl:hasPolicy                                               |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 만약 ODRL 어휘([ODRL-VOCAB](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-odrl-vocab))를 사용하는 자원과 관련있는 right들을 표현하는 정책. |
| Range:        | odrl:Policy                                                  |
| Usage note:   | ODRL([ODRL-VOCAB](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#bib-odrl-vocab)) 정책으로서 표현된 right들에 관한 정보는 *아마도(MAY)* 자원을 위해 제공되어질 것이다. |

#### 6.4.22 Property: is referenced by

| RDF Property: | dct:isReferencedBy                                           |
| ------------- | ------------------------------------------------------------ |
| Definition:   | publication, reference cite, 또는 다른 catalog화된 자원을 가리키는 것과 같은 관계 자원. |
| Usage note:   | data 인용의 use case와 관련되어, catalog화된 자원이 데이터셋일 때, dct:isReferencedBy 특성은 데이터셋을 가리키거나 인용하는 자원들을 위한 데이터셋과 연관되게 한다. 다수의 dct:isReferencedBy 특성은 다수의 publication 또는 다른 자원들에 의하여 참조되어진 데이터셋을 나타내기 위해 사용될 수 있다. |
| Usage note:   | 이 특성은 질의 안의 자원과 연관시키기 위해 사용된다. 이 특성이 기술되지 않은 자원의 다른 관계를 위해서, 더 많은 generic 특성인 dcat:qualifiedRelation이 사용될 수 있다. |

### 6.6 Class: Dataset

| RDF Class:    | dcat:Dataset                                                 |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 하나 또는 그 이상의 형식으로 접근하거나 다운로드 가능한, 그리고 단일 개체에 의해 publish되고 curate된 데이터의 모음. |
| Sub-class of: | dcat:Resource                                                |
| Usage note:   | 이 class는 개념적인 데이터셋을 기술한다. differing schematic layouts과 형식 또는 serialization들과 함께 하나 또는 그 이상의 표현이 사용 가능하다. |
| Usage note:   | 이 class는 데이터셋 제공자의 의해 publish된 실제 데이터셋을 기술한다. 실제 데이터셋과 catalog가 필요한 데이터셋 간의 차이가 있을 경우, [catalog record](https://www.w3.org/TR/2019/WD-vocab-dcat-2-20190528/#Class:Catalog_Record) class가 마지막을 위해 사용될 수 있다. |

#### 6.6.1 Property: dataset distribution

| RDF Property:    | dcat:distribution                    |
| ---------------- | ------------------------------------ |
| Definition:      | 데이터셋의 사용 가능한 distribution. |
| Sub-property of: | dct:relation                         |
| Domain:          | dcat:Dataset                         |
| Range:           | dcat:Distribution                    |

#### 6.6.2 Property: frequency

| RDF Property: | dct:accrualPeriodicity                                       |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 데이터셋이 publish되는 빈도수.                               |
| Range:        | dct:Frequency                                                |
| Usage note:   | dct:accrualPeriodiciry의 value는 dataset-as-a-whole이 업데이트되는 비율을 가져다준다. 이는 time series에서 모아진 데이터 point들 간의 시간을 가져다주기 위한 dcat:temporalResolution에 의해 보완될 수 있다. |

#### 6.6.3 Property: spatial/geographical coverage

| RDF Property: | dct:spatial                                                  |
| ------------- | ------------------------------------------------------------ |
| Definition:   | 데이터셋에 의해 감싸진 지리학적 범위                         |
| Range:        | dct:Location                                                 |
| Usage note:   | 데이터셋의 지역적 범위는 dct:Location의 instance로서 인코딩되거나 지역을 묘사하는 자원의 URI reference를 사용해 표시될 수 있다. [Geonames](http://www.geonames.org/)와 같이 잘 유지된 gazetteer 안의 link들이 권장된다. |

#### 6.6.4 Property: spatial resolution

| RDF Property: | dcat:spatialResolutionInMeters |
| ------------- | ------------------------------ |
| Definitions:  |                                |
|               |                                |
|               |                                |

