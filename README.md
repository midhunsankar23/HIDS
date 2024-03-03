---  
# HIDS  
  
### Prerequisites  
   
Ensure that you have the following installed on your local machine:  
   
- Python 3.x  
- pip  
- virtualenv  
- Root access on your machine  
   
### Setting Up  
   
Follow these steps to get a local copy of the code:  
   
1. Clone the repository:  
  
    ```  
    git clone https://github.com/midhunsankar23/HIDS.git  
    ```  
   
2. Navigate to the project directory:  
  
    ```  
    cd HIDS  
    ```  
   
3. Create a virtual environment:  
  
    ```  
    python3 -m venv venv  
    ```  
   
4. Activate the virtual environment:  
  
    ```  
    source venv/bin/activate  
    ```  
   
5. Install the required dependencies:  
  
    ```  
    pip install -r requirements.txt  
    ```  
   
### Running the Application  
   
Follow these steps to run the application:  
   
1. Open two terminals with root access:  
  
    ```  
    sudo su  
    ```  
   
2. In both terminals, navigate to the project directory and activate the virtual environment:  
  
    ```  
    source venv/bin/activate  
    ```  
   
3. In the first terminal, run the main application:  
  
    ```  
    python3 app.py  
    ```  
   
4. In the second terminal, setup the `iptables` rules to redirect packets to a Netfilter queue (NFQUEUE):  
  
    ```  
    iptables -I INPUT -j NFQUEUE --queue-num 0  
    iptables -I OUTPUT -j NFQUEUE --queue-num 0  
    ```  
  
    This command sets up `iptables` rules to forward incoming and outgoing packets to a Netfilter queue (NFQUEUE). NFQUEUE is a mechanism that allows userspace processing of packets. Packets that are sent to NFQUEUE are dequeued and read from userspace, where they can be analyzed or modified.  
   
5. Still in the second terminal, run the packet capture script:  
  
    ```  
    python3 packet_capture.py  
    ```  
   
6. After running the application, the `iptables` rules can be cleared to restore normal network activity:  
  
    ```  
    iptables --flush  
    ```  
   
---  