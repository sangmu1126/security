# 통합 명세 1.1 · Security 적용 경계

채택일: 2026-11-14 · 개인 개발 기준. 팀 platform의 API·권한·태스크 변경이 아니다.

원문 정본은 개인 sova-test에 [bytes 그대로 보존](https://github.com/sangmu1126/sova-test/blob/4023ec503c43d00c2f58805628c1c5e2c7d80965/docs/specifications/contract-driven-migration-platform-v1.1-integrated-notion.md)했다. SHA-256은 `ffad2d1f49ea4878bf50b9e08d117e9f722e68197e4dde7e3e769c1f6d171d66`이며 [채택 ADR](https://github.com/sangmu1126/sova-test/blob/4023ec503c43d00c2f58805628c1c5e2c7d80965/docs/adr/0001-contract-driven-foundation.md)을 따른다. 이 저장소에 별도 원문 사본을 만들어 두 기준으로 발전시키지 않는다.

## 이번 단계에서 유지하는 것

Sova는 ServiceContract와 방향별 capability/qualification을 소유한다. Security는 현재의 scope/revision·서명·등록 신뢰·보안 판정·보류/해제 경계를 소유한다. 새로운 검증 레코드 이름이 등장했다고 기존 Evidence/ControlRun을 복제하거나 T10 승인·실행권을 이 패키지로 옮기지 않는다.

`StrategyQualification`의 전체 record 인증 adapter는 아직 운영 등록 저장소에 연결하지 않았다. 현재 Sova 시험의 authenticator는 local double이며 실제 qualification 서명 발급이나 운영 인수를 뜻하지 않는다. 기존 `RegisteredProgramAuthority`/`SignedProgramEvidence`는 자체 typed 증거·현재 등록·키 신뢰를 검증한다. 새 record를 그대로 이 API에 넣는 호환성이 확인된 것은 아니다. 향후 명시적 매핑·인증된 등록과 회수 시험을 붙인다.

package 0.11.1과 소비 producer 고정값은 유지한다. 문서 채택만으로 버전을 올리거나 기존 수용 schema·원장 SQL·신뢰 SHA를 바꾸지 않는다.

## 통제별 재사용과 추가 검증

아래 `MIG:SEC-*`는 새 명세 Part I의 ID다. T5의 동명 `SEC-*`, Part II의 `IAM-*`, 과거 CTRL/POL/SEC-PATCH와 다른 이름 공간이다.

| 새 요구 | 재사용할 기존 책임 | 추가 구현·실환경 인수 |
|---|---|---|
| MIG:SEC-01 조직·서비스별 최소 권한 | ResourceScope, tenant 전용 저장/읽기·RLS, 보호 비교 | 계약 registry와 자격 조회의 객체별 인가·타 고객 실제 거부 |
| MIG:SEC-02 승인된 변경만 허용 | governance/program guards, 현재 증거/보류 재검사 | Sova 고정 계약·manifest와 기존 승인·효과 원장 결속 |
| MIG:SEC-03 비밀 보호 | 제한된 입력·정제된 결과, 평가 입력 서명 | 각 source/로그/AI/빌드 산출물의 실제 누출 점검 |
| MIG:SEC-04 신원·전송 | 판정 서비스 TLS·현재 workload 인증 | 고객 CIAM/워크로드/운영자 신원은 독립 검증, Part II Gate 추가 |
| MIG:SEC-05 실행 격리 | Harbor request와 독립 산출물 계약 | sandbox runtime/egress/노드 경계의 실제 부정 시험 |
| MIG:SEC-06 공급망 | 이미지 보고서·SBOM·고정 source 검사와 산출물 결속 | 승인된 서명 identity/issuer·실제 실행 digest·자격 철회 |
| MIG:SEC-07 감사 보존 | 서명 증거·현재 등록·append-only 보조 기록 | 호스트의 별도 WORM 권한·누락 경보·삭제 거부·보존 인수 |
| MIG:SEC-08 복구 자산 | recovery 검증 의무와 기존 프로그램 evidence | 독립 백업·키 접근·실제 복원·업무·RPO/RTO |
| MIG:SEC-09 API·콘솔 | ASGI 입력/신원/tenant 경계, 정제된 오류 | 새 계약·자격 API의 인증·object authorization·revision CAS |
| MIG:SEC-10 남용·비용 | 문서 크기·시간·연결 수 제한 | 조직별 AI/VM/egress 비용·동시 작업 한도 |
| MIG:SEC-11 위치 | 기존 AI residency의 처리/저장/지원 경로 정책 | 실제 호출·백업·로그·모델/IdP의 위치 증명 |
| MIG:SEC-12 사고 대응 | 독립 SecurityHold·서명 HoldRelease·재검증 | S.2 전체 상태 머신·현장 ACK·사고별 회수·재구축 인수 |

## 다음 기능 순서

1. 명시적 증거 의존성 색인: 자원 UID·프로브/정책/이미지/신원 변경 시 관련 evidence·approval의 재평가.
2. 보안 사고 상태와 SAFE_HOLD 분리: 진행 중 효과를 지우거나 source writer를 자동으로 열지 않는다.
3. 자격 회수의 신규 발급·기존 토큰·기존 세션·하위 접근 네 항목을 별도 기록.
4. Identity·Patching 확장은 기존 원문과 버전 있는 대응표로 추가한다. 실제 계정/원문 인수와 고객 데이터 처리는 별도 승인·범위로 진행한다.

각 단계는 schema/의미 검사 → 거부 사례 → 고정 consumer 계약 → 실제 대상 환경 인수 순으로 확인한다. 로컬 시험·문서 구조를 운영 PASS로 표현하지 않는다.
