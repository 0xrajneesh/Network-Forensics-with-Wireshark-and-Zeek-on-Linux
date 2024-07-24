# Home Lab: Network Forensics with Wireshark and Zeek on Linux

## Introduction

Network forensics involves capturing, recording, and analyzing network traffic to detect and investigate security incidents. This advanced-level lab will guide you through using Wireshark and Zeek to perform network forensics on a Linux system. You will learn to capture network traffic, analyze it for suspicious activities, detect intrusions, and understand the network behaviors.

## Pre-requisites

- Advanced knowledge of Linux operating systems
- Understanding of networking concepts and protocols
- Familiarity with Wireshark and Zeek
- Experience with command-line tools

## Lab Set-up and Tools

- A computer running a Linux distribution (e.g., Ubuntu)
- [Wireshark](https://www.wireshark.org/download.html) installed
- [Zeek](https://docs.zeek.org/en/current/install.html) installed
- Network traffic generator or sample pcap files

### Installing Wireshark

1. Update your package list:
    ```bash
    sudo apt update
    ```
2. Install Wireshark:
    ```bash
    sudo apt install wireshark
    ```

### Installing Zeek

1. Update your package list:
    ```bash
    sudo apt update
    ```
2. Install dependencies:
    ```bash
    sudo apt install cmake make gcc g++ flex bison libpcap-dev libssl-dev python3 python3-dev zlib1g-dev
    ```
3. Download and install Zeek:
    ```bash
    wget https://download.zeek.org/zeek-3.0.0.tar.gz
    tar -xvzf zeek-3.0.0.tar.gz
    cd zeek-3.0.0
    ./configure
    make
    sudo make install
    ```

## Exercises

### Exercise 1: Capturing Network Traffic with Wireshark

**Objective**: Capture live network traffic using Wireshark.

1. Open Wireshark.
2. Select the network interface to capture traffic from (e.g., `eth0` or `wlan0`).
3. Click the "Start Capturing Packets" button (blue shark fin).
4. Perform some network activities (e.g., browsing the web).
5. Stop the capture after a few minutes.
6. Save the captured traffic to a pcap file.

**Expected Output**: A pcap file containing captured network traffic.

### Exercise 2: Analyzing Network Traffic with Wireshark

**Objective**: Analyze the captured network traffic to identify suspicious activities.

1. Open the pcap file in Wireshark.
2. Apply filters to focus on specific types of traffic (e.g., `http`, `tcp`, `dns`).
3. Identify and document any anomalies or suspicious activities in the traffic.
4. Use Wireshark's protocol hierarchy and statistics tools for deeper analysis.

**Expected Output**: A detailed analysis report of the captured network traffic, highlighting any suspicious activities.

### Exercise 3: Setting Up Zeek for Real-Time Network Monitoring

**Objective**: Configure Zeek for real-time network traffic monitoring.

1. Configure Zeek for your network interface:
    ```bash
    sudo nano /usr/local/zeek/etc/node.cfg
    ```
    Update the `interface` line to your network interface (e.g., `eth0`).
2. Deploy Zeek:
    ```bash
    sudo /usr/local/zeek/bin/zeekctl deploy
    ```
3. Verify that Zeek is running and monitoring network traffic:
    ```bash
    sudo /usr/local/zeek/bin/zeekctl status
    ```

**Expected Output**: Zeek configured and running, monitoring real-time network traffic.

### Exercise 4: Detecting Intrusions with Zeek

**Objective**: Use Zeek to detect network intrusions and analyze logs.

1. Generate network traffic that simulates an attack (e.g., using a network traffic generator or replaying a malicious pcap file).
2. Check Zeek logs for any alerts or indicators of compromise:
    ```bash
    sudo cat /usr/local/zeek/logs/current/notice.log
    ```
3. Analyze the logs to understand the nature and source of the intrusion.
4. Document your findings and any indicators of compromise.

**Expected Output**: Detailed log entries of detected intrusions, with an analysis report of the findings.

### Exercise 5: Creating Custom Zeek Scripts for Detection

**Objective**: Develop and deploy custom Zeek scripts to detect specific network activities.

1. Create a custom Zeek script to detect a specific type of network activity (e.g., scanning):
    ```bash
    sudo nano /usr/local/zeek/share/zeek/site/local.zeek
    ```
    Add the script content:
    ```zeek
    event connection_established(c: connection) {
        if ( c$resp_h in Site::local_nets && c$resp_p == 80/tcp ) {
            print fmt("HTTP connection to local network: %s -> %s", c$id$orig_h, c$id$resp_h);
        }
    }
    ```
2. Deploy the script:
    ```bash
    sudo /usr/local/zeek/bin/zeekctl deploy
    ```
3. Generate network traffic that matches the script criteria and verify detection in the logs.

**Expected Output**: Custom detection logs in Zeek, verifying the functionality of the custom script.

## Conclusion

By completing these exercises, you have gained advanced skills in network forensics using Wireshark and Zeek on a Linux system. You have learned to capture and analyze network traffic, configure Zeek for real-time monitoring, detect intrusions, and create custom scripts for specific detections. These skills are essential for performing comprehensive network forensic investigations and enhancing network security.


## About Me

I am a cybersecurity trainer with a passion for teaching and helping others learn essential cybersecurity skills through practical, hands-on projects. Connect with me on social media for more updates and resources:

[![LinkedIn](https://img.icons8.com/fluent/48/000000/linkedin.png)](https://www.linkedin.com/in/rajneeshcyber)
[![YouTube](https://img.icons8.com/fluent/48/000000/youtube-play.png)](https://www.youtube.com/@rajneeshcyber)
[![Twitter](https://img.icons8.com/fluent/48/000000/twitter.png)](https://twitter.com/rajneeshcyber)

Feel free to reach out with any questions or feedback. Happy learning!
