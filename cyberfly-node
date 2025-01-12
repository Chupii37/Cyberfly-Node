#!/bin/bash

# Function to handle errors
handle_error() {
    echo "Error: $1"
    exit 1
}

# Display the logo first
echo "Displaying the logo..."
wget -qO- https://raw.githubusercontent.com/Chupii37/Chupii-Node/refs/heads/main/Logo.sh | bash || handle_error "Failed to display the logo."

# Update and upgrade packages if any updates are available
echo "Checking for updates and upgrading system..."
sudo apt-get update -y && sudo apt-get upgrade -y || handle_error "Failed to update and upgrade the system."

# Check if Docker is installed
echo "Checking if Docker is installed..."
if ! command -v docker &> /dev/null; then
    echo "Docker is not installed. Installing Docker..."
    sudo apt-get install -y docker.io || handle_error "Failed to install Docker."
else
    echo "Docker is already installed."
fi

# Prompt user for Kadena wallet address and private key
read -p "Enter your Kadena wallet address: " your_kadena_wallet_address
read -sp "Enter your node private key: " node_priv_key
echo

# Clone the repository and navigate to the directory
echo "Cloning cyberfly-node-docker repository..."
git clone https://github.com/cyberfly-io/cyberfly-node-docker.git || handle_error "Failed to clone the repository."
cd cyberfly-node-docker || handle_error "Failed to change directory to cyberfly-node-docker."

# Pull the latest changes from the repository
echo "Pulling latest changes from the repository..."
git pull || handle_error "Failed to pull the latest changes."

# Make the start_node.sh script executable
echo "Making start_node.sh script executable..."
sudo chmod +x start_node.sh || handle_error "Failed to make start_node.sh executable."

# Run the start_node.sh script with the provided Kadena wallet address and private key
echo "Starting the Kadena node..."
sudo ./start_node.sh k:$your_kadena_wallet_address $node_priv_key || handle_error "Failed to start the Kadena node."

# Success message
echo "Kadena node setup completed successfully!"
