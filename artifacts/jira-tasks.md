# Jira Tasks Artifact

- **Source:** Requirement Review Artifact (/artifacts/requirement-review.md), Confluence 66031 «Login Requirements»
- **Producer:** Skill task-design
- **Status:** VALID (Quality Gate пройден). Создание новых задач НЕ ВЫПОЛНЕНО: все спроектированные задачи имеют существующие дубликаты в Jira (SCRUM-162…SCRUM-175).
- **Jira project:** SCRUM (TMS). Тип задач: Task. Reporter: Timofei Borodich.

## Дедупликация

При проверке существующих Jira-задач (JQL: `project = SCRUM`) обнаружено 14 задач, созданных 2026-09-10 из этой же страницы требований и покрывающих те же требования (включая идентичные конфликты C-01, C-03, C-04, C-14). В соответствии с AGENT.md («не создавай несколько задач, описывающих одно и то же изменение») новые задачи НЕ создаются. Маппинг ниже фиксирует соответствие спроектированных задач существующим.

## Спроектированные задачи

### T1 — Реализовать форму авторизации с валидацией полей Email и Password
- **Source Requirements:** R2.1–R2.8, R3.2, R3.3, R3.5, R3.7, R3.4/R3.6 (C1)
- **Acceptance Criteria:** AC-2, AC-3, AC-4 (из Requirement Review); конфликт C1 (длина Email 100 vs 120) не превращён в критерий — зависит от решения.
- **Dependencies:** —
- **Priority:** Medium (обоснован риск-фактором валидации; подтверждение владельцем)
- **Duplicate:** **SCRUM-162** (существующий)

### T2 — Реализовать валидацию пароля при авторизации
- **Source Requirements:** R4.1–R4.3, R4.5–R4.7; C15 (легаси 6 vs 8 символов)
- **Acceptance Criteria:** V-7, V-8, V-9; легаси-исключение (R4.4) помечено как требующее решения C15.
- **Dependencies:** T1
- **Priority:** Medium
- **Duplicate:** **SCRUM-163** (существующий)

### T3 — Реализовать обработку успешной и неуспешной авторизации
- **Source Requirements:** R5.1, R5.2, R5.5, R6.5, R6.6; конфликты C2 (редирект /admin vs /dashboard) и C3 (сообщения об ошибках)
- **Acceptance Criteria:** AC-1, AC-5; фактический редирект и набор сообщений — зависят от решений C2/C3, помечены как требующие решения.
- **Dependencies:** T1, T2
- **Priority:** High (бизнес-критичность авторизации)
- **Duplicate:** **SCRUM-164** (существующий)

### T4 — Реализовать контроль неуспешных попыток входа, блокировку и сброс счётчика
- **Source Requirements:** R7.1–R7.7; конфликт C4 (3 попытки/30 мин vs 5 попыток/15 мин vs неограниченно)
- **Acceptance Criteria:** V-10, BR-6, BR-7; пороги и длительность блокировки — требуют решения C4.
- **Dependencies:** T3
- **Priority:** High (защита от перебора)
- **Duplicate:** **SCRUM-165** (существующий)

### T5 — Реализовать обработку авторизации в зависимости от статуса учётной записи
- **Source Requirements:** R8.1–R8.5, R9.1–R9.5; конфликты C5 (BLOCKED) и C6 (INACTIVE)
- **Acceptance Criteria:** V-11, V-12; поведение BLOCKED/INACTIVE — требуют решения C5/C6.
- **Dependencies:** T3
- **Priority:** High (права доступа)
- **Duplicate:** **SCRUM-166** (существующий)

### T6 — Реализовать пользовательскую сессию, срок действия и завершение по бездействию
- **Source Requirements:** R10.1–R10.8; конфликт C7 (15 vs 30 минут бездействия)
- **Acceptance Criteria:** AC-6, V; таймаут бездействия — требует решения C7.
- **Dependencies:** T3
- **Priority:** High (управление сессиями)
- **Duplicate:** **SCRUM-167** (существующий)

### T7 — Реализовать опцию Remember Me
- **Source Requirements:** R11.1–R11.6, R10.7; конфликт C8 (запрет для Administrator vs доступность всем ролям)
- **Acceptance Criteria:** PF-5; доступность для Administrator — требует решения C8.
- **Dependencies:** T3, T6
- **Priority:** Medium
- **Duplicate:** **SCRUM-168** (существующий)

### T8 — Реализовать восстановление пароля через ссылку на Email
- **Source Requirements:** R12.1–R12.10; конфликт C9 («Email not found.» vs скрытие существования Email)
- **Acceptance Criteria:** PF-6; сообщение при незарегистрированном Email — требует решения C9.
- **Dependencies:** T1
- **Priority:** Medium
- **Duplicate:** **SCRUM-169** (существующий)

### T9 — Реализовать Logout
- **Source Requirements:** R13.1–R13.4; конфликт C10 (все сессии vs только текущая)
- **Acceptance Criteria:** PF-7, R13.2; объём завершаемых сессий — требует решения C10.
- **Dependencies:** T3, T6, T12 (JWT)
- **Priority:** High (управление сессиями)
- **Duplicate:** **SCRUM-170** (существующий)

### T10 — Реализовать управление параллельными сессиями
- **Source Requirements:** R14.1–R14.5; конфликт C11 (максимум 3 vs только 1 активная)
- **Acceptance Criteria:** BR; лимит сессий — требует решения C11.
- **Dependencies:** T3, T6
- **Priority:** Medium
- **Duplicate:** **SCRUM-171** (существующий)

### T11 — Реализовать определение роли и контроль доступа
- **Source Requirements:** R15.1–R15.6
- **Acceptance Criteria:** PF-10, NF-11, R15.5, R15.6
- **Dependencies:** T3
- **Priority:** High (права доступа)
- **Duplicate:** **SCRUM-172** (существующий)

### T12 — Реализовать выдачу и обновление Access и Refresh токенов
- **Source Requirements:** R16.1–R16.7; конфликт C12 (одноразовый vs продолжающий действовать Refresh Token)
- **Acceptance Criteria:** PF-9; политика ротации Refresh Token — требует решения C12.
- **Dependencies:** T3
- **Priority:** High (безопасность)
- **Duplicate:** **SCRUM-174** (существующий)

### T13 — Реализовать требования производительности и обработку ошибок сервиса авторизации
- **Source Requirements:** R19.1–R19.5, R20.1–R20.4; конфликт C14 (5 сек vs Timeout при 3 сек)
- **Acceptance Criteria:** AC-7, NF-9, NF-10; пороги времени ответа — требуют решения C14.
- **Dependencies:** T3
- **Priority:** Medium
- **Duplicate:** **SCRUM-173** (существующий)

### T14 — Реализовать требования безопасности и аудит авторизации
- **Source Requirements:** R17.1–R17.6, R18.1–R18.5; конфликт C13 (пароль в application logs vs логи безопасности)
- **Acceptance Criteria:** AC (HTTPS, токены не в URL, пароль не в API), R18; политика логирования пароля — требует решения C13.
- **Dependencies:** T3
- **Priority:** High (безопасность)
- **Duplicate:** **SCRUM-175** (существующий)

## Результат этапа Jira

- Новые Jira-задачи НЕ создавались (обнаружены полные дубликаты).
- Фактически существующие задачи (идентификаторы сохранены): **SCRUM-162, SCRUM-163, SCRUM-164, SCRUM-165, SCRUM-166, SCRUM-167, SCRUM-168, SCRUM-169, SCRUM-170, SCRUM-171, SCRUM-172, SCRUM-173, SCRUM-174, SCRUM-175**.
- Все задачи имеют статус «К выполнению», приоритет Medium, reporter Timofei Borodich.

## Blockers / Open Questions (наследуются из Requirement Review)

- C1: длина Email 100 vs 120.
- C2: редирект Administrator → /admin vs /dashboard.
- C3: набор сообщений об ошибке авторизации.
- C4: порог/длительность блокировки по попыткам.
- C5: возможность входа BLOCKED.
- C6: возможность входа INACTIVE.
- C7: таймаут бездействия 15 vs 30 минут.
- C8: Remember Me для Administrator.
- C9: сообщение при незарегистрированном Email (восстановление).
- C10: объём завершаемых сессий при Logout.
- C11: лимит параллельных сессий.
- C12: политика ротации Refresh Token.
- C13: логирование пароля.
- C14: порог времени ответа.
- C15: легаси-пароли 6+ символов.

## QA Conclusion (Task Design Gate)

- Каждая спроектированная задача имеет основание в Requirement Review. ✅
- Значимые требования покрыты задачами. ✅
- Acceptance Criteria не содержат придуманных бизнес-правил; конфликтные критерии помечены как требующие решения (не превращены в готовые). ✅
- Traceability сохранена (Source Requirements, конфликты). ✅
- Необоснованные дубликаты отсутствуют (новые задачи не созданы, существующие зафиксированы). ✅
- Jira-операции создания не выполнялись — создание не требуется, так как целевые задачи уже существуют.