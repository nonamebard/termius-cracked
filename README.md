Termius Patch Guide

https://img.shields.io/badge/Educational-Use%2520Only-red.svg
https://img.shields.io/badge/%E2%9A%A0%EF%B8%8F-Disclaimer-critical.svg
📋 Overview

This guide demonstrates how to modify Termius application files to enable premium features. For educational purposes only.
⚠️ Important Notice

This guide is provided for educational and research purposes only.

    Modifying software may violate the Terms of Service

    Always support developers by purchasing legitimate licenses

    Use at your own risk

    No warranty or support provided

🛠️ Prerequisites

Ensure you have Node.js installed, then install the asar utility:
bash

npm install -g asar

🖥️ For Windows Users

The process is similar to macOS. Follow the instructions below, adjusting paths for your Windows installation (typically in Program Files).
🍎 For macOS Users
Step 1: Extract Application Files
bash

# Navigate to Termius application directory
cd /Applications/Termius.app/Contents/Resources/

# Extract the application archive
asar extract app.asar ./app

# Backup original file (recommended)
mv app.asar app.asar.bak

# Prevent automatic updates
rm app-update.yml

Step 2: Modify Background Process

Edit the file: app/js/background-process.js

    Search for: await this.api.bulkAccount

    Find the line: const e=await this.api.bulkAccount();

    Replace with: var e=await this.api.bulkAccount();

    Insert the following code block immediately after that line:

javascript

// Premium activation configuration
e.account.pro_mode = true;
e.account.need_to_update_subscription = false;
e.account.current_period = {
    "from": "2022-01-01T00:00:00",
    "until": "2099-01-01T00:00:00"
};
e.account.plan_type = "Premium";
e.account.user_type = "Premium";
e.student = null;
e.trial = null;
e.account.authorized_features.show_trial_section = false;
e.account.authorized_features.show_subscription_section = true;
e.account.authorized_features.show_github_account_section = false;
e.account.expired_screen_type = null;
e.personal_subscription = {
    "now": new Date().toISOString().slice(0, -5),
    "status": "SUCCESS",
    "platform": "stripe",
    "current_period": {
        "from": "2022-01-01T00:00:00",
        "until": "2099-01-01T00:00:00"
    },
    "revokable": true,
    "refunded": false,
    "cancelable": true,
    "reactivatable": false,
    "currency": "usd",
    "created_at": "2022-01-01T00:00:00",
    "updated_at": new Date().toISOString().slice(0, -5),
    "valid_until": "2099-01-01T00:00:00",
    "auto_renew": true,
    "price": 12.0,
    "verbose_plan_name": "Termius Pro Monthly",
    "plan_type": "SINGLE",
    "is_expired": false
};
e.access_objects = [{
    "period": {
        "start": "2022-01-01T00:00:00",
        "end": "2099-01-01T00:00:00"
    },
    "title": "Pro"
}];

Important: Preserve the existing return statement and surrounding code structure.
Step 3: Complete Setup

    Launch Termius application

    Log into your account

    Restart Termius completely

    Verify premium features are now available

🔧 Troubleshooting
Issue	Solution
Permission denied	Use sudo or check file permissions
asar not found	Verify npm installation with npm list -g asar
Changes not applied	Restart computer and relaunch Termius
Syntax errors	Check JavaScript code for typos
📝 Notes

    Application updates will overwrite these modifications

    This method may stop working with future Termius updates

    Consider using official Termius subscription for guaranteed functionality

    Backup important data before making any changes

📜 License & Disclaimer

This repository is for educational purposes only. The author does not condone software piracy. Users are responsible for complying with all applicable laws and software licenses. If you find Termius useful, please support the developers by purchasing a subscription.
🤝 Contributing

This guide is provided as-is. Issues related to the modification process may be discussed, but no guarantees of functionality are provided.

Last Updated: 2024 | Educational Use Only

https://img.shields.io/badge/Support_Developers-Buy_Termius_License-green.svg