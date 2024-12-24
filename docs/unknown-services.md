# Unknown services

## Use nmap with scripts
```sh
nmap -sC -sV -p <port> <target>
```

## Netcat (nc)
Netcat allows you to send and receive data manually to ports.

```sh
nc <target> <port>
```

Type commands like HELP, INFO, or random input to provoke a response.

You can manually send a payload or HTTP request:

```bash
echo "GET / HTTP/1.1" | nc <target> <port>
```

## Telnet
Telnet is similar to Netcat but specifically designed for testing and interacting with text-based services.

```sh
telnet <target> <port>
```

## Curl/Browser
Visit the port in the browser to see if it has a web interface.

## Analyze traffic
Use Wireshark or tcpdump to capture traffic on the port while it is in use. Look for protocol patterns or specific keywords that indicate the type of service. 

!!! note "What you can see"

    This option is typically intended when you're on the same network as the target machine. If you can sniff traffic depends on the network topology. If two machines are on the same subnet and communicate directly (via ARP-based communication), their traffic may not pass through a router. If the communication involves devices on different subnets, the traffic must pass through a router. In the case you are on a different subnet, the traffic you can see is limited.

```sh
sudo tcpdump -i eth0 port <port>
```

If you're on a different subnet, traffic must pass through a router or a Layer 3 switch to reach other subnets. The visible traffic depends on the router configuration. Routers isolate traffic between subnets. Broadcast and multicast traffic does not cross subnets. But you can sniff traffic from devices in your local subnet going to the port you want to investigate. Nowadays, most networks use switches which forward packets only to the destination device (ARP poisoning has to be performed in this case).

## Research
Publicly search what runs on the particular port. https://speedguide.net