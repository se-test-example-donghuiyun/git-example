# Git 分支（Branch）操作指南

分支（Branch）是 Git 中用於平行開發、隔離不同功能或修復 Bug 的核心機制。在獨立分支上開發不會影響主要分支（如 `main` 或 `master`）的穩定性。

---

## 1. 檢視分支

* **檢視本機所有分支**（前面帶有 `*` 代表目前所在分支）：
  ```bash
  git branch

```

* **檢視本機與遠端（Remote）所有分支**：
```bash
git branch -a

```


* **檢視各分支最後一次 Commit 訊息**：
```bash
git branch -v

```



---

## 2. 建立分支

* **僅建立新分支**（仍停留在當前分支）：
```bash
git branch <branch-name>

```


* **建立新分支並立即切換過去**（推薦，新版 Git）：
```bash
git switch -c <branch-name>

```


* **建立新分支並切換**（傳統指令）：
```bash
git checkout -b <branch-name>

```



---

## 3. 切換分支

* **切換至已存在的分支**（推薦）：
```bash
git switch <branch-name>

```


* **切換至已存在的分支**（傳統指令）：
```bash
git checkout <branch-name>

```



---

## 4. 合併分支（Merge）

將功能分支的成果整合回主分支：

1. 先切換回目標主分支（例如 `main`）：
```bash
git switch main

```


2. 執行合併：
```bash
git merge <feature-branch>

```



> **注意**：如果主分支與功能分支修改了相同檔案的相同行數，會產生 **衝突（Conflict）**。需手動解決衝突、儲存檔案後執行 `git add .` 與 `git commit` 完成合併。

---

## 5. 推送與追蹤遠端分支

* **首次將本機分支推送到遠端（GitHub）並建立追蹤**：
```bash
git push -u origin <branch-name>

```


* **後續在該分支推送更新**：
```bash
git push

```



---

## 6. 刪除分支

* **刪除已合併的本機分支**（安全刪除）：
```bash
git branch -d <branch-name>

```


* **強制刪除未合併的本機分支**：
```bash
git branch -D <branch-name>

```


* **刪除遠端 GitHub 上的分支**：
```bash
git push origin --delete <branch-name>

```



---

## 7. 常用開發流程示範

```bash
# 1. 確保本地 main 是最新狀態
git switch main
git pull

# 2. 開發新功能：建立並切換到 feature-login 分支
git switch -c feature-login

# 3. 進行程式修改、加入暫存並提交
git add .
git commit -m "feat: 完成登入功能"

# 4. 推送到遠端儲存庫
git push -u origin feature-login

# 5. 開發完成後切回 main 合併
git switch main
git merge feature-login

# 6. 推送更新後的 main 到遠端，並清理本機分支
git push origin main
git branch -d feature-login