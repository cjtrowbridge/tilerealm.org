# tilerealm.org
A decentralized, tile-based fantasy game that enables users to collaboratively explore the realms that exist within their devices and create complex real-world systems that can do anything.

Welcome to the project! Check out the `realms.json` file. This is the core component of the game's backend infrastructure. It contains all the information needed to represent different "realms" (or levels) within a given device, as well as the network of local and remote peers (each containing its own reallms). Players can modify and traverse through these realms and create complex networks of logic which enable them to do literally anything, in the real world. The realms.json file is essential for understanding how the game world is structured and how it connects to a broader network of devices, each hosting its own unique realms and services. Let's break it down so you can get started with building a new front-end for exploring these realms and interacting with other users.

### Overview of the `realms.json` Structure

The `realms.json` file is divided into several key sections:

1. **Realms**:
   - **Definition**: This section defines the different realms (or levels) within the local device. Each realm is essentially a grid-based world that players can explore.
   - **Structure**:
     - **gridSize**: Defines the number of rows and columns in the grid.
     - **defaultBackground**: The background texture used for tiles that do not specify a custom background.
     - **Layers**:
       - **background**: A 2D array representing the background texture for each tile.
       - **foreground**: A 2D array representing the foreground texture for each tile.
       - **passable**: A 2D array of boolean values indicating whether each tile can be traversed by the player or NPCs.
       - **mapTriggers**: A 2D array where each tile can contain triggers that execute actions when a player interacts with them (e.g., teleporting to another realm).
       - **players**: Specifies the current positions of players within the realm.
       - **npcs**: Specifies the current positions of non-playable characters (NPCs) within the realm.

   - **Usage**: API calls will return an updated version of the state of the realms.json file so that you can paint it with any changes made by NPCs or other users or by logic (spells) running in the realm.

2. **LocalPeers**:
   - **Definition**: This section lists other devices (peers) on the same local network that are hosting their own realms and services. These peers are essentially other instances of the game running on different devices that are discoverable on the local network.
   - **Structure**:
     - **deviceName**: The name of the device hosting the realm.
     - **realm**: The name of the primary realm hosted on that device.
     - **services**: A list of services available on the device (e.g., AI processing, Tor network access, decentralized storage).
     - **capabilities**: Describes the specific hardware or software capabilities available on the device which correspond to objects or features available in those realms.
     - **networkAddress**: The IP address or hostname of the device, allowing the front-end to connect to it.
     - **lastSeen**: A timestamp indicating when the device was last active on the network.

   - **Usage**: This section allows the front-end to discover other devices on the network, show the user what realms and services are available, and enable them to connect and interact with those realms.

3. **RemotePeers**:
   - **Definition**: This section lists remote peers that are not on the local network but can be accessed via the internet using protocols like Tor, IPFS, or HTTP. These peers are other users’ devices hosting realms or services in other parts of the world outside your local network.
   - **Structure**:
     - **peerName**: The name of the remote peer.
     - **realm**: The primary realm hosted by the remote peer.
     - **services**: A list of services available on the remote peer.
     - **address**: The address used to resolve the peer, which varies depending on the protocol (e.g., Tor `.onion` address, IPFS CID, HTTP domain).
     - **lastSeen**: A timestamp indicating when the peer was last active.

   - **Usage**: This section enables the front-end to connect to realms hosted on remote devices across the internet, expanding the game's universe beyond the local network. It allows users to explore and interact with realms hosted by other players globally.

### How to Use This Information in the Front-End

When building the front-end for this project, you'll need to:

1. **Render the Game World**:
   - Use the data in the `realms` section to render the grid-based world for each realm.
   - Implement player movement and interaction based on the `passable` and `mapTriggers` arrays.
   - Display the appropriate background and foreground textures for each tile.

2. **Enable Local Network Interaction**:
   - Use the `localPeers` section to display a list of discoverable devices on the local network.
   - Allow users to select a device and connect to its realms or services.
   - Handle authentication if required.

3. **Support Remote Peer Connections**:
   - Use the `remotePeers` section to display a list of remote devices that can be accessed over the internet.
   - Enable users to connect to these remote peers and explore their realms.
   - Handle different protocols (Tor, IPFS, HTTP) to ensure proper connectivity and interaction.

4. **Manage State and Interactions**:
   - The front-end should be able to handle updates to the game state as players move between realms or interact with different peers.
   - Use the `lastSeen` timestamps to indicate the availability of devices and peers, helping users understand which realms are currently accessible.


Here’s the detailed plan for the next steps, focusing on the development and release of the three initial versions for 0.1:

### **Next Steps**

I am working on two initial releases which will allow a wide variety of use cases and runtime environments while using minimal dependencies, in order to enable rapid development across platforms with minimal resource requirements. 

#### **C++ Server Development (Version 0.1)**
   - **Objective**: Develop a robust and high-performance server in C++ that handles the core game logic and interactions. This server will be accessed via a web browser.
   - **Tasks**:
     - **Set Up the Server Environment**: Configure the C++ environment to support multi-threaded operations and real-time interactions.
     - **Implement Core Game Logic**: Develop the functions for managing realms, processing player movements, executing map triggers, and handling peer interactions.
     - **Web Browser Interface**: Create a lightweight web interface that connects to the C++ server, allowing users to explore realms, interact with objects, and communicate with peers.
     - **Testing and Optimization**: Perform stress tests to ensure the server can handle multiple users concurrently, and optimize for low-latency performance.
   - **Release**: Package the server and web interface for deployment, providing clear instructions for users to connect via their browsers.
   - **Note**: Version 0.1 of the C++ server is only targeting linux. 

#### **Java App Development (Version 0.1)**
   - **Objective**: Develop a cross-platform Java app that runs on Android, iOS, and Windows. The app can be accessed either by a web server or through a traditional gaming front-end.
   - **Tasks**:
     - **Set Up the Java Development Environment**: Configure the necessary tools for cross-platform development, such as Android Studio and JavaFX.
     - **Implement Cross-Platform Game Logic**: Develop the game’s core functions in Java, ensuring compatibility across mobile and desktop platforms.
     - **Integrate with Web Servers**: Ensure the Java app can connect seamlessly to both the C++ and PHP servers, providing a consistent user experience regardless of the platform.
     - **Create a Traditional Gaming Front-End**: Develop a traditional gaming interface for the app, with controls optimized for both touchscreens and keyboards.
     - **Testing on Multiple Platforms**: Rigorously test the app on Android, iOS, and Windows devices to ensure smooth operation and a consistent user experience.
   - **Release**: Publish the Java app on relevant platforms (Google Play, App Store, etc.) and provide instructions for accessing the game via web servers or the traditional front-end.
