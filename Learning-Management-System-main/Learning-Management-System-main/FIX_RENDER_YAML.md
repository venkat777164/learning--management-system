# Fix: Add render.yaml to GitHub

Render can't find `render.yaml` because it's not committed to your GitHub repository yet.

## Quick Fix Steps:

1. **Open your terminal/command prompt** in the project root (where `backend` and `frontend` folders are visible).

2. **Check if render.yaml exists:**
   ```bash
   dir render.yaml
   # or
   ls render.yaml
   ```

3. **Add and commit render.yaml:**
   ```bash
   git add render.yaml
   git commit -m "Add render.yaml for Render deployment"
   ```

4. **Push to GitHub:**
   ```bash
   git push origin main
   ```

5. **Go back to Render** and click the **"Retry"** button.

---

## Alternative: Create render.yaml directly on GitHub

If the file isn't in your local repo, you can create it on GitHub:

1. Go to your GitHub repo: `https://github.com/venkat777164/learning--management-system`
2. Click **"Add file"** → **"Create new file"**
3. Name it: `render.yaml`
4. Copy and paste this content:

```yaml
services:
  - type: web
    name: lms-backend
    env: java
    rootDir: backend
    buildCommand: ./mvnw -DskipTests package
    startCommand: java -jar target/Learning-Management-System-0.0.1-SNAPSHOT.jar
    plan: free
    autoDeploy: true
    envVars:
      - key: JAVA_VERSION
        value: 21
      - key: SPRING_PROFILES_ACTIVE
        value: default
    healthCheckPath: /actuator/health
    headers:
      - path: /*
        name: Access-Control-Allow-Origin
        value: "*"
```

5. Click **"Commit new file"** (commit to `main` branch)
6. Go back to Render and click **"Retry"**

---

After this, Render should detect your `render.yaml` and set up the deployment automatically!

