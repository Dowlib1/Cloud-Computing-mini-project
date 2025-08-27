Throughout this mini project, I learned the critical differences between infrastructure environments and environment variables, and how each plays a unique role in software development and deployment. By developing the `aws_cloud_manager.sh` script, I gained hands-on experience in creating dynamic scripts that adapt to local, testing, and production environments using environment variables and command-line arguments. This approach enabled me to build flexible automation tools that can securely and efficiently manage cloud resources across various stages of the software lifecycle, reinforcing the importance of modular, maintainable, and environment-aware scripting practices in cloud engineering.
# aws_cloud_manager.sh - Shell Script for Managing Cloud Infrastructure Across Environments

## Script

```bash
#!/bin/bash

# Check if an argument is provided
if [ "$#" -eq 0 ]; then
    echo "Usage: $0 <environment>"
    echo "Please specify one of: local, testing, production"
    exit 1
fi

# Set ENVIRONMENT variable from the first argument
ENVIRONMENT="$1"

# Act based on the environment argument
if [ "$ENVIRONMENT" == "local" ]; then
    echo "Running script for Local Environment..."
    # Place local environment commands here
elif [ "$ENVIRONMENT" == "testing" ]; then
    echo "Running script for Testing Environment..."
    # Place testing environment commands here
elif [ "$ENVIRONMENT" == "production" ]; then
    echo "Running script for Production Environment..."
    # Place production environment commands here
else
    echo "Invalid environment specified. Please use 'local', 'testing', or 'production'."
    exit 2
fi
```

## How to Use

1. **Make the script executable**  
   ```bash
   sudo chmod +x aws_cloud_manager.sh
   ```

2. **Run the script with an environment argument:**  
   ```bash
   ./aws_cloud_manager.sh local
   ./aws_cloud_manager.sh testing
   ./aws_cloud_manager.sh production
   ```

3. **Expected output examples:**  
   - If you run `./aws_cloud_manager.sh testing`, you get:
     ```
     Running script for Testing Environment...
     ```
   - If no argument is provided:
     ```
     Usage: ./aws_cloud_manager.sh <environment>
     Please specify one of: local, testing, production
     ```
   - If you run with an invalid argument:
     ```
     Invalid environment specified. Please use 'local', 'testing', or 'production'.
     ```

## Explanation

- The script requires you to specify the environment (`local`, `testing`, or `production`) as a command-line argument.
- It sets the `ENVIRONMENT` variable from your argument and runs the appropriate logic for the specified environment.
- This prevents hard-coding, supports dynamic execution, and demonstrates best practices for environment-aware scripting.

## Notes

- You can add environment-specific AWS CLI commands under each block for actual cloud management tasks.
- This script fulfills the project requirement to show practical code and use of positional parameters for dynamic environment selection.
