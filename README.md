# Deploy Key Generation Guide

This guide will help you generate and add a deploy key to your GitHub repository.

## Step 1: Generate SSH Key

1. Open your terminal.
2. Run the following command to generate a new SSH key. Replace `<comment>` with a comment that helps you identify the key later (e.g., your email address or a description of the key's purpose).

    ```sh
    ssh-keygen -t rsa -b 4096 -C "<comment>"
    ```

3. When prompted to save the key, press Enter to accept the default file location or specify a different path if you prefer.
4. Optionally, enter a passphrase for added security.

## Step 2: Copy the SSH Key

1. Run the following command to copy the public key to your clipboard:

    ```sh
    cat ~/.ssh/id_rsa.pub
    ```

2. Manually copy the output or use `pbcopy` if you are on macOS:

    ```sh
    pbcopy < ~/.ssh/id_rsa.pub
    ```

## Step 3: Add the SSH Key to GitHub

1. Go to your GitHub repository page.
2. Navigate to **Settings** > **Deploy keys**.
3. Click **Add deploy key**.
4. In the **Title** field, add a descriptive name for the key.
5. Paste your public key into the **Key** field.
6. Optionally, check the "Allow write access" box if needed.
7. Click **Add key** to save.

## Step 4: Verify the SSH Key

1. Run the following command to verify that the SSH key is added and working correctly:

    ```sh
    ssh -T git@github.com
    ```

2. If the setup is correct, you should see a message similar to:

    ```
    Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
    ```

## Step 5: Using the Deploy Key

1. In your deployment scripts or CI/CD pipeline configuration, use the SSH URL of your repository:

    ```sh
    git@github.com:reegancorp/deploy-key-demo.git
    ```

2. Ensure the SSH agent is running and has the key added:

    ```sh
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
    ```

3. Your deployment process should now be able to clone and pull from the repository using the deploy key.

That's it! You have successfully generated and added a deploy key to your GitHub repository.
