# Sample repo for testing EvalsHub CI/CD (webhook)

Use this folder as a minimal GitHub repo to test EvalsHub’s CI webhook. When you push, GitHub sends a webhook to EvalsHub, which runs your configured experiment and records the run.
 son
**Quick start:** Copy the entire `ci-webhook-test` folder to a new directory (or use it inside the EvalsHub repo), create a new GitHub repo, then follow the steps below.
ddj
## 1. Create a new GitHub repo

- On GitHub: **New repository** (e.g. `evalshub-ci-test`).
- Do **not** add a README or .gitignore (we’ll push this folder).

## 2. Configure CI in EvalsHwub
x
1. In **EvalsHub**: go to **Settings →qq CI / CD**.
2. **Step 1**: Pick a project, prompt, dataset, and scorers (or create them first).
3. **Step 2**: Click **Create CI key** and **copy the key** (you’ll use it as the webhook secret).sss
4. **Step 3**: Copy the **Wewbhook URL** (it looks like  
   `https://<your-evalshub-host>/api/ci/webhook?projectId=...&experimentId=...`).

## 3. Push this sample to your repo

From this folder (or the repo root after you’ve copied these files in):

```bash
git init
git add .
git commit -m "Initial commit: sample for EvalsHub CI webhook"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

Replace `YOUR_USERNAME` and `YOUR_REPO_NAME` with your GitHub user/org and repo name.

## 4. Add the webhook in GitHub

1. Open your repo on GitHub → **Settings → Webhooks → Add webhook**.
2. **Payload URL**: paste the Webhook URL from EvalsHub (step 2 above).
3. **Content type**: `application/json`.
4. **Secret**: paste your EvalsHub CI key (from step 2).
5. **Which events**: choose **Just the push event**.
6. Click **Add webhook**.

## 5. Trigger a run

Make a small change and push:

```bash
# e.g. edit index.js or add a file
echo "// test" >> index.js
git add index.js
git commit -m "Trigger CI webhook"
git push
```

Then in EvalsHub go to **Settings → CI / CD** and check the **CI runs** table. You should see a new run with your commit and branch.

## 6. (Optional) Set a baseline

After the first successful run, click **Set as baseline** on that run. Future pushes will then pass or fail based on whether the score regresses below the threshold (default 5%).

---

**Files in this sample**

- `index.js` – minimal script so there’s something to commit and push.
- `package.json` – so the repo looks like a small Node project.
- This `README.md` with the steps above.

You can add more files or change the app; any push to the repo will trigger the webhook.
