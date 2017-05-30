![Supported Python versions](https://img.shields.io/badge/python-2.7-blue.svg)
# WiFiSuite     
	WiFiSuite was developed to perform Brute-force attacks against Access Points (AP) configured 
	with Extensible Authentication Protocol (EAP) using an Active Directory database. 
	If clients/probes were configured to check for server side certificates the traditional 
	EvilTwin attack vector would no longer be feasible, and a second attack vector would need to exists.

	Often Pentesters perform brute-force attacks on internal engagements against hosts running the 
	Server Message Block (SMB) service. Common EAP configurations use the same usernames and passwords 
	as an SMB service would on the internal network.
	
	WiFiSuite leverages the commonality between EAP and SMB by performing a brute-force attack against 
	Access Points running EAP with an Active Directory database. The type of brute-force attack is 
	tailored to perform a single password guess across a list of user accounts, this particular style
	of brute-force attack if often called a ‘Password Spray’

## :heavy_exclamation_mark: Requirements
	Kali 2016.1 or Kali 2016.2 rolling. 
	External WiFi card, known working Brands/Models: TP-Link Model TL-WN722N, AWUS036NH, AWUS051NH
    
## Installation
	apt-get install scapy
	git clone https://github.com/NickSanzotta/WiFiSuite.git
	cd WiFiSuite
	python setup.py install --record install.log	
##
	cd wifisuite/
	python wifisuite.py
	Output of Successful Installation:
	       [i] Directory found: data/
 	       [!] Database not found: data/WiFiSuite.db
 	       [i] Created Datebase: data/WiFiSuite.db
 	       [i] Database instantiated

## Uninstall
    cd WiFiSuite
    cat install.log | xargs rm -rf

## Dependencies
    netifaces
    python-pip 
    python-dev
    psutil
    scapy    
    wpa_supplicant
    
## Installation troubleshooting
    Error(s) Rasised: Bad key "patch.force_edgecolor"
    Resolution: pip install matplotlib --upgrade
    
    Error: You received an 'Attribute' error, while running WiFiSuite ENUM.
    Resolution: apt-get install scapy (Even if Scapy is already installed on Kali 2016.2)
    

## Average Brute-force time per WiFi Interface
    While developing this tool, I discovered Brute-force timings may be dependent upon 
    Operating System, Signal Stregnth and Wireless Interface Make/Model.
    Below are some rough estimates based on my testing:
    
    Raspberry Pi 3 Model B w/ Raspbian
    Elapsed Time with failure: 3.9s - 4.0s
    Elapsed Time with Success: 0.9s - 1.0s
    
    TP-Link Model TL-WN722N w/ Kali 2016.2 Virtual Machine
    Elapsed Time with failure: 6.0s - 6.1s
    Elapsed Time with Success: 2.8s - 2.9s
    
    Alfa Model AWUS036NH w/ Kali 2016.2 Virtual Machine
    Elapsed Time with failure: 6.8s - 6.9s
    Elapsed Time with Success: 3.6s - 3.7s
    
    Alfa Model AWUS051NH v.2 w/ Kali 2016.2 Virtual Machine
    Elapsed Time with failure: 14.7s - 14.9s
    Elapsed Time with Success: 11.3s - 11.6s


## :book: Cheat Sheet
    * SCAN:           python wifisuite.py -iwlan0 scan --location="CoffeeShop"
    * ENUM:           python wifisuite.py -iwlan0 -d 10:10:10:A9:72:E6 -c4 enum --seconds=30 --packets=5
    * SPRAY (EAP):    python wifisuite.py -iwlan0 -s"RadiusX" -u data/users.txt -pWelcome1 spray
    * SPRAY (WPA):    python wifisuite.py -iwlan0 -s"CompanyXYZ Hotspot" -p data/passwords.txt spray
    * CONNECT (EAP):  python wifisuite.py -iwlan0 -s"RadiusX" -ubeamr -pWelcome1 connect
    * CONNECT (WPA):  python wifisuite.py -iwlan0 -s"CompanyXYZ Hotspot" -p Password123 connect
    * CONNECT (Open): python wifisuite.py -iwlan0 -s"CompanyXYZ Hotspot" connect
    * MAC (Randomize):python wifisuite.py -iwlan0 mac
    * MAC (Manual):   python wifisuite.py -iwlan0 -m 10:10:10:A9:72:E6 mac
    * DATABASE:       python wifisuite.py database
    
##
* SCAN: Perform a quick survey of the 2.4Ghz Wireless Spectrum
     ![](https://github.com/NickSanzotta/img/blob/master/WiFiSuiteSCAN-C.gif)
##
* ENUM: Capture “user identities” from Access Points running PEAP EAP. This module will send de-authentication packets to the 	      desired Access Point and then sniff for clear text user identities.
     ![](https://github.com/NickSanzotta/img/blob/master/WiFiSuiteENUM-A.gif)
##
* SPRAY (EAP): Perform a EAP Password Spray against across a list of user accounts using a single password.
	       [*] Tip SSID(s) are case sensitive!
	       
     ![](https://github.com/NickSanzotta/img/blob/master/WiFiSuiteSPRAYEAP-A.gif)
##

* CONNECT (EAP): Connect to an EAP Access Point with username and password authentication, after connection has completed 
		 open a new console tab to interact with the network. Shutdown connection cleanly to avoid future 			 connectivity issues.
	         [*] Tip SSID(s) are case sensitive!

     ![]( https://github.com/NickSanzotta/img/blob/master/WiFiSuiteCONNECT-A.gif)

## :octocat: Credits
	Contributor(s):             Bill Harshbarger 'https://github.com/bharshbarger'
	Inspiration (Database):     byt3bl33d3r 'https://github.com/byt3bl33d3r/CrackMapExec'
	Beta Testers:               jstines, sho-luv, dissect0r

## Disclaimer

***WiFiSuite is intended to be used for legal security purposes only, any other use is not the responsibility of the developer(s). ***