## ⭐Benchmarking of Variant Annotation Tools⭐
2024_Bioinfomatics_project

## 👉Member
한국외국어대학교 바이오메디컬공학부 <br>
202202358 이나림 <br>
202202665 이은서

## 👉프로젝트 개요
본 프로젝트는 SIFT, CADD, ANNOVAR와 같은 변이 분석 도구를 사용하여 환자군 데이터를 기반으로 변이를 평가하고, 각 도구에서 제공된 점수를 비교하여 주요 해로운 변이를 식별하는 것을 목표로 합니다.

## 👉필수 요구사항

#### **소프트웨어 및 패키지**
1. Python (>= 3.8)
2. ANNOVAR
   - 공식 웹사이트에서 다운로드 후 설치: [ANNOVAR 공식 사이트](http://www.openbioinformatics.org/annovar/)
3. CADD
   - CADD 설치 및 실행을 위해 [CADD 설치 가이드](https://cadd.gs.washington.edu/) 참고.
4. SIFT
   - [SIFT 설치 가이드](http://sift.jcvi.org/)에서 소프트웨어 다운로드 및 환경 구성.

## 👉프로그램 실행 방법

### 1. 데이터 준비
- `/MG_VCF` 디렉토리에 환자의 VCF 파일을 추가합니다. 예시 파일은 `P1300NJS_F.vcf`, `P1301JWY_M.vcf` 등으로 구성됩니다.

### 2. SIFT, CADD, ANNOVAR 분석 수행
#### **SIFT 실행**
```bash
java -jar ./SIFT4G_Annotator.jar -c -i MG_VCF/P1300NJS_F.vcf -d ./databases/GRCh37.74/ -r output2
```

#### **CADD 실행**
```bash
./CADD.sh -c 8 -a -g GRCh37 ../../sift4g-re/sift4g/MG_VCF/P1300NJS_F.vcf
```

#### **ANNOVAR 실행**
```bash
table_annovar.pl P1300NJS_F.avinput humandb/ -buildver hg19 -out P1300NJS_F_anno -remove -protocol refGene,cytoBand,exac03,avsnp147,dbnsfp30a -operation gx,r,f,f,f -nastring . -csvout -polish -xref example/gene_xref.txt
```

### 3. 결과 통합 및 시각화
위의 코드를 통해 vcf파일을 필터링 후 프로젝트를 진행하였습니다.

함께 추가한 소스코드를 통해 결과를 확인하고, 시각화를 진행하였습니다.



## 👉결과 확인
  
1) SIFT, CADD, ANNOVAR 
00 번 환자에 대해 SIFT, CADD, ANNOVAR 세가지 분석 툴을 사용해 얻은 SIFT 점수 분포를 비교하였습니다.
2) SIFT, ANNOVAR 
01번 환자에 대해 SIFT, ANNOVAR 두가지 분석 툴을 사용해 얻은 SIFT 점수 분포를 비교하였습니다.


## 👉주요 내용

- ANNOVAR 데이터와 SIFT 데이터의 차이점 : ANNOVAR 데이터는 점수 0.000에서 22.34%를 
차지하며 가장 집중된 변이를 보이는 반면, SIFT 데이터는 9.50%로 점수 0.000에 대한 집중도가 
낮습니다. 점수 0.001 ~ 0.008의 구간에서는 두 데이터 세트가 비슷한 경향을 보이지만 SIFT 
데이터에서의 변이 비율이 ANNO 데이터에 비해 다소 낮게 나타납니다.

## 👉기타 참고사항

- 자세한 프로젝트 방법론 및 결과(시각화결과)는 `ProjectReport_이나림_이은서.pdf` 파일 및 코드를 통해 확인 가능합니다.
