# The Internet

- [What is the Internet?](#what-is-the-internet)
- [How does the Internet work?](#how-does-the-internet-work)
- [What is the web?](#what-is-the-web)
- [What is a resource?](#what-is-a-resource)
- [What is the client-server model?](#what-is-the-client-server-model)
  - [Server-side Infrastructure](#server-side-infrastructure)
- [PDU](#pdus)
- [Internet Function](#internet-function)


## What is the Internet?

The internet is a "network of networks". A network is any number of devices that are connected in order to exchange data. The internet consists of a massive number of small, localized networks (known as LANs) connected to each other via routers. When we say "The Internet", we are describing: the physical infrastructure that facilitates this interconnectivity, as well as the protocols that control its functionality.

## How does the Internet work?

The Internet can be thought of as a series of different "layers" operating on top of one another: from the physical infrastructure on the lowest level to the protocols that control message syntax at the highest level. All of these layers working together facilitate _networked communication_. Each layer is governed by some sort of _protocol_, or system of rules, that allows it to perform a service to encapsulated data from the layer above. In other words, a PDU of a protocol at a higher layer is *encapsulated* in a PDU of a protocol at the current layer.

When a user types a URL into an address bar, such as `www.google.com`, this triggers the _client_ (usually the browser) to send an HTTP request for the resource indicated by the address. HTTP is the protocol functioning at the highest layer, the _Application Layer_, and it controls the structure of messages exchanged between networked applications. It packages data into a PDU (protocol data unit) known as a Request or a Response. A Request is sent to a certain server to request a particular resource from the web. This might be a webpage, an image, or video file.

A URL is a specifically formatted Universal Resource Locator that helps HTTP figure out how and where to send the request. It includes the _domain_ of the requested resource, i.e. `www.google.com`. Once the HTTP request is processed into a data unit, that domain name is handed to DNS (Domain Name Service). DNS consists of a distributed database that lives on a multitude of DNS servers. The domain name gets handed to one of these servers, whose job it is to map it onto the corresponding IP address. Because an IP address is just a series of numbers, a domain name allows us to have a more human-friendly version of the server location.

A URL also includes a port number. A port number can be explicitly specified, otherwise the default port used. The IP address and the port number _together_ allow the protocols operating in the Transport Layer to facilitate data exchange between specific applications running on separate devices across the network. This is usually governed by either TCP or UDP.

With TCP, the HTTP request is encapsulated into the data payload of a TCP segment. This segment contains metadata about the source and destination port numbers that allows it to be routed to the correct process running at the other end. It also facilitates something known as the TCP handshake, which provides reliability in the form of acknowledging the transmitted message, retransmission of messages that get dropped, and in-order delivery of fragmented data. However, due to the complexity of this step, it can contribute to the overall latency of the trip. UDP, on the other hand, provides more speed at the cost of reliability. With UDP, daya is encapsulated in the form of a UDP datagram.

That TCP packet is then again encapsulated into the data payload of the PDU operating at the Internet / Network Layer, known as an IP packet. This facilitates communication between _hosts_ (aka computers) on different networks, through the use of the IP address provided by DNS. These come in two different flavors, IPv4, which is a 32-bit address, and IPv6, which is an 128-bit address. Because IP addresses are logical and hierarchical they are well suited to communication over a large distributed network.

The IP packet is responsible for routeing all the encapsulated data on its journey, which consists of a series of network "hops" between various nodes (routers) on the overall network. It contains data that pertains to the source and destination IP address, so that a route can be determined, as well as data pertaining to the packets TTL or Time To Live. This is the maximum number of "hops" a packet is allowed to take. If the number is reached, the IP packet gets dropped from the network!

Next, the Link / Data Link Layer takes over, usually by implementing Ethernet Protocol and encapsulating the IP packet into an Ethernet Frame. The Ethernet protocol provides two main functions: _framing_, which provides logical structure to the streams of bits traveling through the physical infrastructure of the network, and _addressing_ which identifies the next network "node" to which data should be sent with the use of MAC addressing.

A MAC address is a physical "burned-in" address that specific to a network _device_ rather than location. Ethernet, therefore, governs communication between devices in a local network, and is responsible for navigating to the correct _physical_ address, rather than logical address (IP's job). For this reason, it acts as an interface between the physical infrastructure below it and the more logical layers above.

Finally, that Ethernet Frame is handed to the Physical Layer, the lowest layer in our networked communications model. This consists of the tangible physical parts that make up the network, i.e. network devices, cables, and wires. These transport all previous encapsulated data as bits in the form of radio waves, light waves, or electrical signals. The physical limitations of networked communication, _latency_ and _bandwidth_, come as a result of unavoidable physical laws that govern this layer.

Once our data is transported to it's destination, a `google.com` server, each layer of networked communication is "unwrapped" in turn so that the original message, the data within the HTTP request, can be processed. When the server receives this, it issues an HTTP response back to the client, which undergoes the same encapsulation and travel process the request did to get from the issuing server back to your browser. If the response is successful, it will include the requested resource in its _body_, which can be rendered in a user friendly way by the browser. If it is unsuccessful, it will respond with some kind of error code, such as 404, which indicates the resource in question was not found, or 500, which indicates a generic server-side error.

This response gets encapsulated into each layer in turn, in order to return to the user. The response will be folded into a TCP segment so that the correct process on your computer can be reached, then an IP packet so the correct network address can be reached, an Ethernet Frame so the correct device can be recognized, and finally down into the binary streams of data being transported across the physical medium of the network. Once it's received by your browser, the browser can process the response and display the website for you! Then, the next user action, clicking a link, opening your e-mail, streaming a game or video starts the whole process all over again.

Encapsulation enables protocols at different layers to work together by providing separation and creating a certain level of abstraction — the protocol at the current layer can provide a 'service' for the protocol at the higher layer, without concerning about any protocol-specific information of the higher-layer protocol.
This is particularly pertinent when there are many different protocols used at one network layer (e.g., protocols at the Application layer include HTTP, SMTP, FTP, and more; a protocol at the Transport layer does not need to know about which protocol it services).

One of the functions in categorizing protocol groups into separate layers is the ability to encapsulate data. Ostensibly, what we are doing is hiding data away within layers, by encapsulating it within a data unit of the layer below. A layer is mostly concerned with it's _header_, that is, the meta-data attached to it's data payload that tells it what to do. It doesn't really matter what the data payload _is_ as long as the header information is complete and the layer can perform its intended function. This means that a protocol at one layer doesn't need to know anything at all about how protocols in other layers are implemented in order for them to interact.

## What is the web?

The **web** (aka World Wide Web) is a service that can be accessed via the internet, not the internet itself. It is essentially a compilation of various _resources_ that can be accessed by means of a URL. Applications are able to interact with these resources by means of HTTP in the Application layer. The Internet provides both the physical infrastructure and the protocols that facilitate the transportation of these various resources to different devices across the world.

### What is a resource?

What is the role of a resource in the general scheme of networked communication?

- Resource is a generic term for any number of things that a user interacts with on the internet that can be retrieved by means of a URL (and therefore an HTTP request). This can include:
  - images, videos, web pages, files, software, games
- Resources make up the web.
- There are no limits to the number of resources.
- A resource is the thing that we, the user, interact with via the client (browser).
- All of the layers of the networked communication model provide their various services, so that we can see/hear/click/interact with the _remote_ resource from any location via the internet.

## What is the client-server model?

- The client-server model is one in which two devices transmitting data over the network each have a role.
- The client generally describes some kind of web-browser. They are responsible for issuing HTTP requests and processing the responses such that they are readable for humans (such as rendering the HTML of a web page).
- The server is a remote computer capable of handling inbound requests. Their job is to issue an HTTP response, which ideally will contain the resource requested by the client, or, if not, will contain some kind of messaging that explains what happened.
- The server in this model is not limited to a single device. In reality, it refers to all the server-side infrastructure that processes the requests and provides the responses.

### Server-Side Infrastructure

- The three primary pieces of server-side infrastructure are the _web server_, the _application server_, and the _data store_.
- **Web server** = responds to requests for static resources, i.e. resources that do not require data processing (like CSS files)
- **Application server** = handling more complicated requests, such as those that contain application or business logic. Any server-side application code lives here.
- **Data store** = some kind of storage construct that can save data for later retrieval and processing.

## PDUs
### What is a Protocol Data Unit (PDU)? What is its purpose in the context of network communication?

* Protocol Data Unit
* a block of data that gets transported over the network by the current "governing" protocol
* The unit itself depends on the layer in which we are currently functioning
* A PDU consists of a _header_ which contains meta-data specific to the current protocol's responsibility / service
* A PDU has a _data payload_ which contains the entire PDU from the layer above the current layer
* It facilitates encapsulation of data, allowing each protocol to operate a modularized process, and perform the service that it is allocated in conjunction with the other protocols that make up the network.

**Caution!** higher-level vs higher layer are two different concepts

### How do the different parts of a PDU interact?

* PDU consists of a header, data payload, and an optional footer.
* Header contains metadata concerning the current protocol, and this metadata facilitates the service the protcol is performing for the data payload.
* Data payload contains the data that the current protocol wants to transport. Specifically, the payload is the PDU of a higher layer.

## Internet Function
What is the primary function of the Internet / Network Layer? What Protocols govern this function?

* This layer is concerned with communication between devices on different networks (i.e., inter-network communication).
* It comes between protocols at the Link/Data Link layer and protocols at the Transport layer.
* The primary protocol that governs this function is the Internet Protocol (IP).

* IP provides routing capabilities between devices on different networks via IP addresses.
* It also encapsulates data in packets.
