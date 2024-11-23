# Grafana Monitoring Dashboard

Grafana is an open-source analytics and interactive visualization platform. It provides dashboards for metrics collected from various data sources like Prometheus, Loki, and more.

---

## 📦 Setup Instructions

### Prerequisites
- Docker and Docker Compose installed on your system.
- Basic knowledge of Docker containers and networking.

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/ashkanramedani/grafana.git
   cd grafana

2. Start the Grafana service using Docker Compose:
   docker-compose up -d

3. Access Grafana in your browser at:
   http://<YOUR_SERVER_IP>:3000

4. Login with the default credentials:
   Username: admin
   Password: admin

🛠 Configuration
Environment Variables
You can customize Grafana by editing the docker-compose.yml file. Here are some key environment variables:

GF_SECURITY_ADMIN_USER: Set the admin username (default: admin).
GF_SECURITY_ADMIN_PASSWORD: Set the admin password (default: admin).
GF_USERS_ALLOW_SIGN_UP: Enable or disable user sign-ups (default: false).

Volume Mapping
Grafana data is persisted using Docker volumes. Ensure that the grafana_data volume is backed up regularly to avoid data loss.
volumes:
  - grafana_data:/var/lib/grafana

Data Sources
To add data sources automatically, use Grafana's provisioning feature. Add a file under grafana/provisioning/datasources/ with the following structure:
apiVersion: 1
datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://prometheus:9090
    isDefault: true
    
Restart the Grafana container to apply these changes.

📊 Creating Dashboards
After logging in, navigate to Dashboards > New Dashboard.
Add a new panel and select your data source (e.g., Prometheus).
Use PromQL queries to fetch data and visualize it (e.g., CPU usage, memory usage).
Save the dashboard for later use.

🔒 Security Best Practices
Update Default Credentials: Change the default admin password immediately after login.
Enable HTTPS: Use a reverse proxy (e.g., Nginx, Traefik, or Caddy) to secure Grafana with SSL.
Limit User Access: Configure roles and permissions for users to prevent unauthorized access.

🤝 Integration with Prometheus
Grafana works seamlessly with Prometheus. To add Prometheus as a data source:

Go to Configuration > Data Sources > Add Data Source.
Select Prometheus.
Enter the URL (e.g., http://prometheus:9090).
Save and test the connection.

🚀 Advanced Features
Alerting
Grafana supports alerting based on metrics:

Go to a panel and configure an alert rule.
Set conditions, frequency, and notification channels (e.g., email, Slack).
Dashboard Import
You can import pre-built dashboards:

Navigate to Dashboards > Import.
Upload a JSON file or use a dashboard ID from Grafana's public repositor.

Plugins
Grafana supports a wide range of plugins for additional data sources, visualizations, and alerts. Install plugins via the CLI:
grafana-cli plugins install <plugin-name>
