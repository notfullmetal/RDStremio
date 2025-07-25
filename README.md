# Real-Debrid + Mediaflow + AIOStreams Deployment Guide

This guide will walk you through the process of deploying the Real-Debrid + Mediaflow + AIOStreams project. Please follow each step carefully to ensure a successful setup.

---

## 1. Configure Environment Variables

Open the `aiostreams.env` file in your project directory. You **must** edit the following lines to match your deployment:

- **Line 20: `BASE_URL`**
  - Set this to the public URL where your addon will be accessible.
  - Example: `BASE_URL=https://aiostreams.yourdomain.com`

- **Line 29: `SECRET_KEY`**
  - This is a critical security setting. Generate a 64-character hex string (see the comment in the file for generation instructions) and set it here.
  - Example: `SECRET_KEY=01234567...........9abcdef`

- **Line 34: `ADDON_PASSWORD`**
  - Set a password to protect your addon installation and usage. This can be any string.
  - Example: `ADDON_PASSWORD=your_strong_password`

---

## 2. Set Password in `mediaflow.env`

Open the `mediaflow.env` file and set a strong password for the MediaFlow service. This is important for securing your stream proxy.

- Example:
  ```env
  API_PASSWORD=your_mediaflow_password
  ```

---

## 3. Add VPN WireGuard Configuration

To route traffic securely, you need to add your VPN's WireGuard configuration file to the project directory:

- Obtain your `wg0.conf` file from your VPN provider.
- Place the `wg0.conf` file in the **same directory** as your other environment files (`aiostreams.env`, `mediaflow.env`).
- This file will be used by the Docker containers to establish a secure VPN connection.

---

## 4. Deploy with Docker Compose

Once all configuration files are set up, you can deploy the project using Docker Compose:

1. Make sure [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) are installed on your system.
2. In your project directory, run:
   ```sh
   docker compose up -d
   ```
   This command will build and start all necessary containers in the background.

3. Check the logs to ensure all services are running correctly:
   ```sh
   docker compose logs -f
   ```

---

## 5. Import AIOStreams Configuration

The `aiostreams-config.json` file allows you to quickly set up your AIOStreams instance with your preferred settings and services. Follow these steps to import your configuration:

1. **Access the AIOStreams Web Interface:**
   - Open your browser and go to the URL you set as `BASE_URL` in your `aiostreams.env` file (e.g., `https://aiostreams.yourdomain.com`).

2. **Navigate to the Configuration Import Section:**
   - In the AIOStreams interface, look for the **"Saves & Install"** section, usually found at the bottom left of the sidebar.

3. **Import the Configuration File:**
   - Click the **"Import"** button.
   - Select the `aiostreams-config.json` file from your project directory.
   - Click the **"Import"** button to finalize the import process.

4. **Enter Your Configuration Password:**
   - Enter the password you will use to log in to the AIOStreams web interface.
   - Click the **"Create"** button.

5. **Retrieve Your Addon Installation URL:**
   - After a successful import, the interface will provide you with an **Install URL**.
   - Copy this URL.

6. **Add the Addon to Stremio:**
   - Open Stremio, go to the **Addons** tab, and paste the Install URL to add your AIOStreams addon.

**Important Reminders:**
- Before importing, ensure you have:
  - Added your Real-Debrid credentials in the **Services** tab of the web interface.
  - Entered the correct Mediaflow Proxy URL and password in the **Proxy** tab.
- You can always update these settings after import if needed.

**Editing Your Configuration in the Future:**
- To edit your configuration later, you will need to log in to the AIOStreams web interface using your **UUID** and the **configuration password** you set during import. Make sure to keep these credentials safe.


## Additional Notes

- **Updates:** If you change any environment variables or configuration files, restart the containers:
  ```sh
  docker compose down
  docker compose up --build -d
  ```

---

You are now ready to use AIOStreams! Enjoy your secure and feature-rich streaming experience. 