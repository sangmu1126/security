# Security 문서 목차

이 저장소는 **공통 보안 패키지와 선택형 보안 판정 서비스**를 제공한다. 승인·운영 변경·워크로드 이동은 소비 플랫폼의 책임이다. Sova 전체 콘솔·실행기를 이 저장소에서 제공하는 것으로 설명하지 않는다.

## 2026-11-14 이후 개발

[통합 명세 적용 경계](contract-driven-adoption.md): 기존 Evidence·보안 보류·승인 책임을 유지하면서 새 ServiceContract/Qualification과 연결하는 순서. 원문은 개인 Sova에 한 번만 보존한다.

## 처음 읽는 순서

| 목적 | 문서 | 기준 |
|---|---|---|
| 두 보안 제안서와 Patching as a Service | [설계 통합](architecture-integration.md), [지속 개선 계약](security-modernization.md) | 요구사항→코드→검증 경계를 추적. AI·Harbor 전체 실행 완료 아님 |
| 패키지 설치·공급망 | [배포 산출물](distribution.md), [통합·소유권](integration.md) | 현재 pyproject 0.11.1. 버전만 같다고 source·wheel·이미지가 같은 것은 아님 |
| 서비스 API·인증·DB | [보안 판정 서비스](security-review-service.md) | 직접 ASGI/Uvicorn, `POST /v1/program-reviews`. 실행 권한 부여 안 함 |
| 실제 팀 플랫폼 인수 준비 | [인계 현황](platform-handoff-status.md), [읽기 전용 인수](platform-readonly-intake.md), [변경 시험 조건](platform-live-acceptance.md) | 11/7 준비 기록. 현재 배포·접속은 새 관측 필요 |
| T14·T33 원문 제출 준비 | [맥 인수 안내](mac-t14-t33-intake.md) | 오프라인 요약은 인수 PASS나 서명 인증을 만들지 않음 |
| 가장 후속인 공개 로컬 인수 결과 | [0.11.1 인수 증빙](evidence/security-intake-2026-11-07/README.md) | 0.11.0 이미지 검사·90분 시험과 producer를 구분 |

## 결과를 합치지 않는 규칙

- 20개 T5 통제 시험, 22개 추가 보안 검사, 12개 platform 소비 기준은 서로 다른 집합이다.
- 서비스 이미지 0건은 기록된 source·아키텍처·scanner DB의 결과다. Sova 대응 앱 이미지나 현재 배포의 검사 결과를 대신하지 않는다.
- `4511a43`의 90분 지속 시험을 `546f6e0` 또는 후속 0.11.1 이미지의 90분 결과로 표기하지 않는다.
- 보안 검토 결과는 T10 승인·잠금, T19 판정, T31/T12 실행·복구를 대체하지 않는다.
- Ready·정책 선언·로컬 JSONL·통과한 CI를 실제 접근 거부·영속 감사·복원 완료로 세지 않는다.

## 저장소 안내

- [Sova Security](<../README.md>) · `README.md`

## 설계 결정 기록 (ADR)

- [ADR-0001: 제한된 보안 판정 서비스와 기존 플랫폼 집행](<adr/0001-security-review-service.md>) · `docs/adr/0001-security-review-service.md`
- [ADR-0002: 서비스 DB 자격을 한 테넌트로 제한](<adr/0002-tenant-fixed-service-reader.md>) · `docs/adr/0002-tenant-fixed-service-reader.md`
- [ADR-0003: 요청 단위 연결과 현재 증거 묶음 검증](<adr/0003-request-scoped-live-evidence.md>) · `docs/adr/0003-request-scoped-live-evidence.md`
- [ADR-0004: 실제 로컬 Kubernetes 인증 계약 검증](<adr/0004-local-kubernetes-authentication.md>) · `docs/adr/0004-local-kubernetes-authentication.md`
- [ADR-0005: 플랫폼 T7와 서비스 전용 자격의 audience 경계](<adr/0005-service-credential-audience.md>) · `docs/adr/0005-service-credential-audience.md`
- [ADR-0006: 현재 경로 묶음 조회와 고정 타입 정보 재사용](<adr/0006-bounded-live-route-reads.md>) · `docs/adr/0006-bounded-live-route-reads.md`
- [ADR-0007: 고정 소스와 최소 입력으로 서비스 이미지 검증](<adr/0007-commit-bound-service-image.md>) · `docs/adr/0007-commit-bound-service-image.md`
- [ADR-0008: 서비스 토큰의 단일 용도와 원래 수명 제한](<adr/0008-service-token-use-boundaries.md>) · `docs/adr/0008-service-token-use-boundaries.md`
- [ADR-0009: 테이블 밖의 서비스 DB 권한도 검증](<adr/0009-indirect-database-privileges.md>) · `docs/adr/0009-indirect-database-privileges.md`
- [ADR-0010: 현재 전체 증거 검증의 결합 계약](<adr/0010-current-collection-authentication.md>) · `docs/adr/0010-current-collection-authentication.md`
- [ADR-0011: TLS 요청 전체의 공통 시간·HTTP 부가 정보 한도](<adr/0011-shared-http-network-deadline.md>) · `docs/adr/0011-shared-http-network-deadline.md`
- [ADR-0012: 관리 함수 EXECUTE도 읽기 전용 역할의 권한 경계다](<adr/0012-restricted-database-routines.md>) · `docs/adr/0012-restricted-database-routines.md`
- [ADR-0013: 자격 교체와 철회의 장시간 실제 프로세스 시험](<adr/0013-owned-process-endurance.md>) · `docs/adr/0013-owned-process-endurance.md`
- [ADR-0014: 실제 서비스 이미지의 OS·Python 취약점 관측](<adr/0014-service-image-vulnerability-evidence.md>) · `docs/adr/0014-service-image-vulnerability-evidence.md`
- [ADR-0015: 부분 기록이 남은 로컬 감사 파일의 신규 판정 보류](<adr/0015-torn-local-audit-records.md>) · `docs/adr/0015-torn-local-audit-records.md`
- [ADR-0016: 감사 기록 이후 원본 권한의 최종 재검사](<adr/0016-authority-after-review-receipt.md>) · `docs/adr/0016-authority-after-review-receipt.md`
- [ADR-0017: DB 전체 역할과 데이터베이스별 접속 경계](<adr/0017-database-specific-reader-ingress.md>) · `docs/adr/0017-database-specific-reader-ingress.md`
- [ADR-0018: 자격 전달 전에 DB 경로와 TLS 설정 검증](<adr/0018-validate-database-routing-before-connect.md>) · `docs/adr/0018-validate-database-routing-before-connect.md`
- [ADR-0019: 전용 보안 DB의 임시 테이블·대형 객체 생성 제한](<adr/0019-reader-storage-creation-boundaries.md>) · `docs/adr/0019-reader-storage-creation-boundaries.md`
- [ADR-0020: 전용 reader의 DB 연결 수 상한](<adr/0020-reader-connection-budget.md>) · `docs/adr/0020-reader-connection-budget.md`
- [ADR-0021: 플랫폼 정본을 소비하는 오프라인 인수 목록](<adr/0021-offline-platform-acceptance-intake.md>) · `docs/adr/0021-offline-platform-acceptance-intake.md`

## 구현·배포·보안 계약

- [두 보안 제안서의 구현과 검증 연결](<architecture-integration.md>) · `docs/architecture-integration.md`
- [평가 입력의 서명 인증 연결](<assessment-input-signatures.md>) · `docs/assessment-input-signatures.md`
- [팀 탐지 계약 연결](<detection-integration.md>) · `docs/detection-integration.md`
- [검증한 wheel 소비](<distribution.md>) · `docs/distribution.md`
- [CISA KEV의 양성 근거 연결](<exploitation-intelligence.md>) · `docs/exploitation-intelligence.md`
- [Harbor 실행·독립 검증 연결 계약](<harbor-contract.md>) · `docs/harbor-contract.md`
- [보안 보류 해제의 승인 서명](<hold-release-signatures.md>) · `docs/hold-release-signatures.md`
- [통합 및 소유권](<integration.md>) · `docs/integration.md`
- [OPA 실행 전 정책 계약](<opa-policy.md>) · `docs/opa-policy.md`
- [기존 생산자 증거와 프로그램 실행 연결](<program-evidence-integration.md>) · `docs/program-evidence-integration.md`
- [Prowler 구성 점검 보고서 연결](<prowler-integration.md>) · `docs/prowler-integration.md`
- [지속 보안 개선 계약](<security-modernization.md>) · `docs/security-modernization.md`
- [제한된 보안 판정 서비스](<security-review-service.md>) · `docs/security-review-service.md`
- [팀 통제 결과와 보안 패키지 연결](<team-control-integration.md>) · `docs/team-control-integration.md`

## 팀 platform 연결과 운영 인수

- [데모용 맥에서 이어받기](<demo-mac-handoff.md>) · `docs/demo-mac-handoff.md`
- [맥 T14·T33 인수 실행 준비](<mac-t14-t33-intake.md>) · `docs/mac-t14-t33-intake.md`
- [플랫폼 통제와 두 제안서의 22개 검사 대응](<platform-control-traceability.md>) · `docs/platform-control-traceability.md`
- [플랫폼 보안 연동 인계 현황](<platform-handoff-status.md>) · `docs/platform-handoff-status.md`
- [실제 플랫폼 인수 실행안](<platform-live-acceptance.md>) · `docs/platform-live-acceptance.md`
- [플랫폼 읽기 전용 인수 목록](<platform-readonly-intake.md>) · `docs/platform-readonly-intake.md`

## 개발·조사 이력

- [Mac 인수 준비: 고정 산출물 대조와 플랫폼 차이](<development/mac-acceptance-preparation-2026-11-07.md>) · `docs/development/mac-acceptance-preparation-2026-11-07.md`
- [배포 차단 해소와 플랫폼 인수 후속 작업](<development/security-acceptance-2026-11-07.md>) · `docs/development/security-acceptance-2026-11-07.md`
- [T14·T33 맥 인수 준비와 개인 어댑터 보강](<development/security-intake-2026-11-07.md>) · `docs/development/security-intake-2026-11-07.md`
- [보안 서비스 개발 기록](<development/security-service-2026-11-06.md>) · `docs/development/security-service-2026-11-06.md`
- [사고 조사와 호환 가능한 보강](<incident-research-2026-11-06.md>) · `docs/incident-research-2026-11-06.md`
- [두 설계 문서 연결의 로컬 검증 기록](<validation-2026-11-06.md>) · `docs/validation-2026-11-06.md`

## 코드·이미지·시간이 고정된 검증 증빙

- [Mac 인수 준비 증거](<evidence/mac-acceptance-preparation-2026-11-07/README.md>) · `docs/evidence/mac-acceptance-preparation-2026-11-07/README.md`
- [SELECT reader의 임시 테이블·대형 객체 생성: 수정 전후](<evidence/reader-storage-2026-11-06/README.md>) · `docs/evidence/reader-storage-2026-11-06/README.md`
- [Native 컨테이너 90분 지속 시험](<evidence/review-container-endurance-2026-11-07/README.md>) · `docs/evidence/review-container-endurance-2026-11-07/README.md`
- [실제 서비스 프로세스의 회전·철회 지속 시험](<evidence/review-endurance-2026-11-06/README.md>) · `docs/evidence/review-endurance-2026-11-06/README.md`
- [T14·T33 로컬 인수 준비 검증](<evidence/security-intake-2026-11-07/README.md>) · `docs/evidence/security-intake-2026-11-07/README.md`
- [서비스 이미지 실제 취약점 검사 — 배포 BLOCK](<evidence/service-image-scan-2026-11-06/README.md>) · `docs/evidence/service-image-scan-2026-11-06/README.md`
- [최종 소비 source의 이미지 검사 원본](<evidence/service-image-scan-2026-11-06/qualified-ec4aac6/README.md>) · `docs/evidence/service-image-scan-2026-11-06/qualified-ec4aac6/README.md`
- [HIGH 49건 이후 이미지 재자격](<evidence/service-image-scan-2026-11-07/README.md>) · `docs/evidence/service-image-scan-2026-11-07/README.md`
- [Alpine 이미지 전체 스캔 PASS (개인 CI)](<evidence/service-image-scan-2026-11-07/qualified-338f755/README.md>) · `docs/evidence/service-image-scan-2026-11-07/qualified-338f755/README.md`
- [T28 운영자 회차 기록의 중단·재시작 경계](<evidence/t28-restart-boundary-2026-11-06/README.md>) · `docs/evidence/t28-restart-boundary-2026-11-06/README.md`

## 문서 점검 기록

- [2026-11-13 재점검](documentation-review-2026-11-13.md): 기준 SHA·수정 이유·검증 범위·미확인 사항.

## 원문·추출 출처·썸네일

- [사고 기반 보안 설계 원문](proposals/incident-security-architecture.txt) · [Patching as a Service 원문](proposals/patching-as-a-service.txt) · [원문 해시](proposals/manifest.json): 사용자 제안서의 원문이다. 원문에 적힌 역사적 사례·제품 상태를 모두 독립 검증했다는 뜻은 아니다. 후속 판단은 구현·조사 문서를 따른다.
- [추출 출처](provenance.json)는 추출 당시 파일 hash다. 이후 수정한 현재 파일과 같아야 하는 잠금 목록으로 쓰지 않는다.
- [썸네일 메타데이터](assets/thumbnail.json): 코드 구조를 그린 설명 이미지이며 운영 실행 증거가 아니다.

검증 폴더의 JSON·로그·SBOM·manifest는 같은 폴더 README가 지정한 producer·해시·시간과 함께 읽는다. 14일 이미지/30일 wheel 보관 정책은 다운로드 가능성을 보증하지 않으며, 만료된 artifact를 동명 다른 버전으로 대체하지 않는다.
