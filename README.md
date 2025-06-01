# African Penguin Protection System
## Overview
The African Penguin Protection System is a comprehensive solution designed to safeguard African penguins from terrestrial predators, specifically Caracals and Honey Badgers, in their coastal habitats. The system integrates detection, deterrence, and analytics to monitor predator activity, activate non-lethal deterrents, and provide actionable insights through a web-based dashboard. Built with modern web technologies, Firebase for real-time data storage, and EmailJS for notifications, it supports conservation efforts by reducing human-wildlife conflict.

## Features
Detection: Utilizes motion-activated cameras and machine learning to identify Caracals and Honey Badgers with confidence scores.
Deterrence: Activates non-lethal deterrents (e.g., ultrasonic sounds, lights) upon confirmed predator detection to protect penguin colonies.
Analytics: Displays real-time and historical predator data via interactive charts, detection logs, and email notifications for conservationists and researchers.
Notification System: Sends email alerts for new detections and configuration confirmations using EmailJS.
Responsive Dashboard: A web interface (stats.html) visualizes detection frequency, time-of-day patterns, and daily trends.
## Tech Stack
Frontend: HTML, Tailwind CSS, Chart.js, JavaScript
Backend: Firebase Realtime Database for storing detection data
Notifications: EmailJS for sending detection and confirmation emails
Detection Hardware: Motion-activated cameras with ML models (not included in this repo)
Deterrence Hardware: Ultrasonic devices and LED lights (not included in this repo)
Fonts: Poppins via Google Fonts
CDN Dependencies:
Firebase SDK v9.22.0
EmailJS SDK v4
Chart.js v4.3.0
Tailwind CSS v3
## Project Structure

├── public/

│   ├── stats.html          # Main dashboard for analytics

│   ├── about.html          # Homepage (placeholder)

│   └── styles/             # Custom CSS (if any)

├── README.md               # This file

└── package.json            # (Optional) Node.js dependencies for local dev

## Setup Instructions
Prerequisites
A Firebase project with Realtime Database enabled
An EmailJS account for email notifications
A GitHub account for hosting the repo
(Optional) A web server (e.g., Firebase Hosting, Netlify) for deployment
Installation
## Clone the Repository
bash

git clone https://github.com/your-username/african-penguin-protection.git
cd african-penguin-protection
## Configure Firebase
Create a Firebase project at console.firebase.google.com.
Enable Realtime Database and copy the Firebase config object.
Update the firebaseConfig in stats.html:
javascript

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
Set database rules to allow reading (adjust for security in production):
json

{
  "rules": {
    "Predator_data": {
      ".read": "true",
      ".write": "auth != null"
    }
  }
}
## Configure EmailJS
Sign up at emailjs.com and create a service.
Create two email templates:
Detection Alert (e.g., template_y094bky): For new detections, using {{animal}}, {{time}}, {{confidence}}.
Confirmation Email (e.g., template_hdmsspc): For notification settings, using {{email}}, {{animals}}, {{minConfidence}}.
Update stats.html with your EmailJS public key and service ID:
javascript

## Production:
Deploy to Firebase Hosting, Netlify, or another platform.
Update EmailJS template links to your hosted URL (e.g., https://your-domain.com/stats.html).
Example for Firebase Hosting:

npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
## Set Up Detection Hardware
Configure ESP32 cameras with ML models to detect Caracals and Honey Badgers.
Push detection data to Firebase under Predator_data/Animal (e.g., "Caracal") and Predator_data/Value (e.g., "0.95").
Ensure timestamps are synchronized (within 10 seconds) for pairing.
## Set Up Deterrence Hardware
Connect ultrasonic devices and LED lights to activate upon confirmed detections (confidence > 85%).
Trigger via a separate script or IoT device listening to Firebase updates (not included).
## Usage
### Detection
How It Works:
Cameras capture motion and run ML models to identify predators.
Detections are pushed to Firebase:
json

Predator_data/Animal/-N1234567890: "Caracal"
Predator_data/Value/-N1234567891: "0.95"
The stats.html script decodes Firebase push IDs to extract timestamps and formats them in SAST (+2 hours).
### Deterrence
Activation:
When a detection’s confidence exceeds 85%, the system triggers deterrents (e.g., ultrasonic sounds, flashing lights).
Controlled via external hardware (not in this repo) listening to Firebase.
Customization:
Adjust the confidence threshold in the dashboard’s notification settings.
### Analytics
Dashboard (stats.html):
Stats: Displays total detections and average confidence for Caracals and Honey Badgers.
Charts:
Pie Chart: Detection frequency by animal.
Scatter Chart: Detections by time of day.
Stacked Bar Chart: Detections by date.
Date Dropdown: Filters data by date to show detailed detection logs.
Detection Tiles: Toggles a list of recent detections (confidence > 85%, max 50).
Notifications:
Enable email notifications via the dashboard.
Set preferences (email, animals to notify for, minimum confidence).
Receive:
Detection Alerts: For new detections matching preferences.
Confirmation Emails: When saving notification settings.
#### Example Workflow
A camera detects a Caracal at 01:49:00 on 2025-05-27 with 95% confidence.
Data is pushed to Firebase.
The stats.html dashboard updates charts and logs.
If notifications are enabled, EmailJS sends a detection alert.
Deterrence hardware activates ultrasonic sounds to deter the predator.
Testing
Firebase:
Add test detections in the Firebase console:
json
Predator_data/Animal/-N1234567890: "Caracal"
Predator_data/Value/-N1234567891: "0.95"
Verify dashboard updates.
### Deterrence:
Simulate a detection and confirm hardware activation (requires custom integration).
License
This project is licensed under the MIT License. See LICENSE for details.

### Acknowledgments
Built for conservation of African penguins.
Uses Firebase, EmailJS, Chart.js, and Tailwind CSS.
Inspired by wildlife protection initiatives in South Africa.
Contact
For issues or inquiries, open a GitHub issue or email jmschl002@myuct.ac.za, jmnsha002@myuct.ac.za, thlboh001@myuct.ac.za.

© 2025 African Penguin Protection System. All rights reserved.
