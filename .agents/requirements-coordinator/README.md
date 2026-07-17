# Requirements Coordinator

這個資料夾保存 `requirements-coordinator-agent` 使用的需求路由資料。

這個設計的目的，是避免 agent 每次處理需求時都讀取所有服務的 `README.md`。agent 應該優先使用這些輕量索引，再只讀取候選服務的最小必要文件。

## 檔案

- `service-index.yml`：workspace 層級的服務 / repo 路由表。
- `contract-registry.yml`：workspace 層級的共用契約註冊表。
- `service-manifest.template.yml`：每個服務可選用的 manifest 範本。

## 建議的服務內檔案

每個服務可以選擇在自己的根目錄加入：

```text
.requirements-agent.yml
```

這個檔案用來描述服務的責任邊界、依賴、契約與需求文件入口。它能讓 coordinator 避免 fallback 到大範圍 README 掃描。


## 需求紀錄格式

需求檔預設放在各服務或專案自己的 `docs/requirements/` 底下，並使用繁體中文記錄。

建議格式：

```markdown
# <需求名稱>

狀態：已提出
負責服務：<Service.Name>

<Service.Name> 需要 <高層需求描述>。

目前預期涵蓋的方向包含：

- <能力或範圍 1>
- <能力或範圍 2>
- <能力或範圍 3>

<與其他服務的責任切分或關聯，如果目前已知。>

詳細資料模型、角色權限、流程、外部整合與 API 契約先延後定義。
```

原則：先記錄需求與責任歸屬，細節不足時不要自行展開；範例應使用中性 placeholder，避免寫入本機路徑或私人環境資訊。

## 更新策略

以下情況建議更新 index：

- 新增服務或 repo。
- 某個服務改變領域概念或資料實體的 ownership。
- 某個服務新增、移除或修改 API。
- 某個服務新增、移除或修改 event。
- 需求文件位置改變。
- 共用 contract 改變。

一般需求處理時，優先透過既有 index 與 registry 路由，不要預設重建整份索引。
