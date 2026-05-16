# Task cards

Task card - это контракт для будущего Codex run.

Каждая task card должна:
- перечислить exact paths обязательных источников;
- указать forbidden substitutes;
- задать runtime baseline;
- объявить stop conditions;
- сказать, готова ли задача к fix-run.

Если required docs имеют `status: stub`, task card должна быть явно не готова.

