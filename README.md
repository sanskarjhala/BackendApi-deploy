# Hello API Deployment Challenge

This project is a simple backend API that exposes a single route `/sayHello` which responds with a JSON message `"Hello User"`. The server runs on **port 80** and is automatically deployed to a remote virtual machine using **GitHub Actions**.

---

## Features

- Express-based backend API
- `/sayHello` GET endpoint
- Runs on **Port 80**
- Automatically deployed to a VM using GitHub Actions and SSH
- No secrets or code pulled manually on the VM
---

## Tech Stack

- Node.js
- Express
- GitHub Actions for CI/CD
- SSH for deployment

---

## API Endpoint

### `GET /sayHello`

**Response:**
```json
{
  "message": "Hello User"
}
```
## Setup Instructions

**1. Clone the Repository**
```bash
  git clone git@github.com:sanskarjhala/BackendApi-deploy.git
  cd BackendApi-deploy
  ```
**2. Install Dependencies**
```bash
    npm install
```
**Run Locally (Optional)**
  ```bash
npm run start
or
node server.js
```
**Then open your browerser and hit this url:**

```bash
http://localhost/sayHello
```
Then open your browser and visit:
**Response:**
```json
{
  "message": "Hello User"
}
```

## GitHub Actions Deployment

Deployment is automated using the workflow file located at:
### 🔁 What the Workflow Does

1. **Installs Node.js** if it's not already installed on the virtual machine.
2. **Kills any previously running instance** of the app to prevent port conflicts.
3. **Installs all project dependencies** using `npm install`.
4. **Starts the app on port 80** using `sudo nohup` to keep it running in the background after the deployment completes.

This ensures that the latest version of your backend API is deployed and accessible after every push to the `master` branch — without requiring manual SSH access or code pulls on the VM.

## How to Test After Deployment
Once you push to master, GitHub Actions will run.

**After successful deployment, open:**
```bash
   http://your_vm_ip/sayHello
    this is mine where its depolyed:  http://20.62.250.175/sayHello
  ```
**Expected response:**
```json
   { "message": "Hello User" }
```

## Challenges Faced

- **Port 80 Access**: Running the app on port 80 required elevated permissions. Since the deployment used a root user, this was handled cleanly using `sudo`.

- **App Stopping After SSH Disconnect**: Initially, the app would stop when SSH was closed. This was resolved by starting the server using `nohup` in the background.

- **No Manual Deployment Allowed**: The challenge required that the code not be manually copied or pulled on the VM. GitHub Actions was used with secure SSH-based deployment to automate everything.


