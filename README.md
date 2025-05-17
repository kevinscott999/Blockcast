#Install docker and docker compose for WINDOWS
```
sudo apt update
sudo apt install -y docker.io docker-compose
sudo systemctl enable docker
sudo systemctl start docker
```

>To run Docker inside WSL or Ubuntu on Windows, you need Docker Desktop for Windows, which exposes Docker to WSL.

> In this Guide, I'll tell you how to Install on Windows using WSL.

## 1. Install Docker Desktop for Windows (if you haven’t):
  • Download it from: https://www.docker.com/products/docker-desktop/
    
## Which One Should You Download?

1. You need AMD64 if:
   • You are on a regular Windows PC or laptop with an Intel or AMD processor.
   • This is the most common setup.

2. You need ARM64 if:
   • You have a Windows device with an ARM processor (like Surface Pro X).
   • These are less common and usually labeled as ARM.

⸻

How to Check Your System Type

To confirm your architecture:
1. Press Windows + I to open Settings.
2. Go to System > About.
3. Look for “System type”:
   • If it says: x64-based processor → Download AMD64
   • If it says: ARM-based processor → Download ARM64
   • During setup, ensure the “Enable WSL and integration” box is checked.

## When you install Docker Desktop for Windows, it includes Docker and Docker Compose for Windows, but that doesn’t always make it available inside WSL (Ubuntu) automatically..

So yes, you still need to run this:
```
sudo apt update
sudo apt install docker-compose-plugin
```
## 2. Restart WSL terminal (or your Ubuntu window), then check Docker:
```
docker --version
docker compose version
```
## Make sure you have Docker installed and running in the background..
> Retrieve the Blockcast Beacon Docker Compose Manifest
```
git clone https://github.com/Blockcast/beacon-docker-compose.git
cd beacon-docker-compose
```

## 3: Launch the BEACON Node

> Start the BEACON services:
```
docker compose up -d
```

> Check the status of the services:
```
docker compose ps
```
You should see services like beacond, blockcastd, and watchtower running...

> If any service isn’t running as expected, view its logs:
```
docker compose logs <service_name>
```
Replace <service_name> with the name of the service you want to inspect...

## 4. Generate Hardware ID and Challenge Key

> Initialize the BEACON node to generate its unique identifiers:
```
docker compose exec blockcastd blockcastd init
```
This command will output:
• Hardware ID: A unique identifier for your device.
• Challenge Key: A Solana-formatted public key unique to your device.
• Registration URL: A link to register your node. ￼

Important: Backup your private key located at ~/.blockcast/certs/gw_challenge.key. Losing this key means you won’t be able to prove ownership of your device..

## 5. Register Your Node

Register your node using the provided URL:
1.Open the Registration URL from the previous step in your browser.

2.Alternatively, visit the Blockcast web portal: https://app.blockcast.network

3. Navigate to Manage Nodes, and click on Register Node. Enter your Hardware ID and Challenge Key manually.
4. Ensure your browser has location access enabled, as it’s required for registration.

After registration:
• Your node should appear as Healthy in the node list within a few minutes.
• Clicking on your node will display details like uptime, connectivity, and rewards information.
• Note: Nodes need to be online for 6 hours for the first connectivity test and 24 hours to start earning rewards.

 
## Lastly, whem your pc goes off, you can Manually Start the BEACON Node After Boot:
```
cd ~/beacon-docker-compose && docker compose up -d
```

## 📌Additional Tips
	•
 1. Port Configuration: Ensure that port 8443 is open and not used by other applications.
 2. Service Management: To stop the BEACON services, run:
```
docker compose down
```

## Monitoring: Regularly check the health and logs of your services to ensure smooth operation.











