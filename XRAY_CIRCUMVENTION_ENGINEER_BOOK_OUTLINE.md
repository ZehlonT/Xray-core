# Xray-core Zero-to-Hero Book Outline

Short description: A beginner-first outline for a future book that starts from basic networking and ends with reading, extending, and contributing to Xray-core.

## How to use this outline
Short description: Each heading is a future chapter or part, and each subheading is a lesson that should explain one idea clearly before moving to the next layer.

### Who this is for
Short description: Readers with little or no networking background who want to understand how modern proxy systems work and how Xray-core is structured.

### What the learner should become
Short description: By the end, the reader should be able to reason about packets, protocols, DPI, censorship resistance, Xray configuration, and code-level contribution paths.

### What this book is not
Short description: It should focus on understanding architecture, protocols, and defensive censorship-resistance concepts rather than giving reckless or misuse-oriented operational playbooks.

## Part I — Why Xray-core exists
Short description: Start with the real-world problem Xray tries to solve, then build the learner's mental model for anti-censorship systems.

### 1. The open internet, control points, and censorship
Short description: Explain who can observe, block, throttle, or manipulate traffic between a user and a destination.

#### 1.1 What “censorship” means on the network
Short description: Define blocking, filtering, throttling, poisoning, traffic shaping, and active probing in simple language.

#### 1.2 Where censors sit in the path
Short description: Show how ISPs, gateways, national firewalls, enterprise middleboxes, and mobile operators can inspect traffic.

#### 1.3 Why ordinary VPN explanations are not enough
Short description: Contrast simple tunnel thinking with the layered protocol and fingerprint-resistance thinking needed for Xray-like systems.

### 2. What Xray-core is
Short description: Introduce Xray-core as a modular traffic processing engine that accepts traffic one way and sends it out another way.

#### 2.1 Xray as a protocol switchboard
Short description: Explain that Xray can combine inbounds, outbounds, routing, transports, and security layers into one flow engine.

#### 2.2 Xray as a platform, not one protocol
Short description: Clarify that Xray-core supports multiple protocol families and transport styles rather than one fixed tunnel design.

#### 2.3 What “anti-censorship” means in Xray terms
Short description: Connect encryption, camouflage, protocol selection, routing, DNS strategy, and fingerprint control into one system goal.

## Part II — Networking from zero
Short description: Build the networking basics needed before any proxy, TLS, or DPI concept makes sense.

### 3. How data moves on a network
Short description: Give the reader a simple end-to-end picture of how information becomes bits, frames, packets, and application messages.

#### 3.1 Clients, servers, and middleboxes
Short description: Introduce the main actors and how each one changes or forwards traffic.

#### 3.2 IP addresses, ports, and sockets
Short description: Explain how machines and applications are identified on a network.

#### 3.3 Packets, streams, and sessions
Short description: Teach the difference between packet-based delivery and stream-based delivery, because Xray works with both.

#### 3.4 Latency, bandwidth, loss, jitter, and congestion
Short description: Cover the network behaviors that make protocol design and transport choice important.

### 4. The layered model without the textbook pain
Short description: Translate OSI/TCP-IP ideas into a practical mental model a builder can actually use.

#### 4.1 Link, network, transport, and application layers
Short description: Show what each layer is responsible for and how layers hide complexity from each other.

#### 4.2 Encapsulation and decapsulation
Short description: Explain how one protocol wraps another and why circumvention systems stack layers.

#### 4.3 Why layers leak fingerprints
Short description: Prepare the reader for DPI by showing that metadata exists at multiple layers, not only in payloads.

## Part III — Core transport protocols
Short description: Teach the transports that all proxy systems must build on top of or work around.

### 5. TCP from first principles
Short description: Explain why TCP is reliable, ordered, and common, but also easy for censors to fingerprint.

#### 5.1 The TCP handshake
Short description: Introduce SYN, SYN-ACK, ACK, and connection state in plain language.

#### 5.2 Reliability, retransmission, and flow control
Short description: Show how TCP repairs loss and why that matters for application behavior.

#### 5.3 Why TCP looks the way it does to DPI
Short description: Connect TCP headers, timing, resets, and flow behavior to censorship visibility.

### 6. UDP from first principles
Short description: Explain why UDP is simple, fast, unordered, and often used when applications want more control.

#### 6.1 Datagram thinking
Short description: Teach the difference between one message at a time and one long stream of bytes.

#### 6.2 Why many modern protocols choose UDP
Short description: Connect UDP to QUIC, media, tunneling, NAT traversal, and low-latency design.

#### 6.3 Why UDP can be both useful and suspicious
Short description: Explain why some networks throttle, block, or rate-limit UDP-heavy traffic.

### 7. QUIC and HTTP/3
Short description: Introduce the modern encrypted transport stack that moves web traffic from TCP+TLS to UDP+QUIC.

#### 7.1 What QUIC changes compared with TCP+TLS
Short description: Show how QUIC merges transport and cryptographic setup into one design.

#### 7.2 Streams inside QUIC
Short description: Explain multiplexing, head-of-line blocking reduction, and why this matters for performance.

#### 7.3 HTTP/3 on top of QUIC
Short description: Describe how HTTP semantics remain while the transport underneath changes.

#### 7.4 What DPI can still see in QUIC
Short description: Explain that encryption hides payloads but still leaves observable metadata, behavior, and fingerprints.

## Part IV — Naming, web protocols, and encryption
Short description: Cover the protocols that reveal intent, identity, and fingerprints even before application data is exchanged.

### 8. DNS and how names become addresses
Short description: Teach why naming is one of the most important visibility points in censorship systems.

#### 8.1 Recursive resolvers, authoritative servers, and caches
Short description: Explain the actors involved in domain resolution.

#### 8.2 DNS leaks, poisoning, blocking, and tampering
Short description: Show why DNS strategy is central to both censorship and circumvention.

#### 8.3 DoH, DoT, and encrypted DNS trade-offs
Short description: Compare encrypted DNS approaches and what they change for privacy, latency, and detectability.

### 9. HTTP, HTTP/2, and HTTP/3
Short description: Explain the web protocols that many camouflage and transport strategies try to resemble or reuse.

#### 9.1 Requests, responses, headers, and bodies
Short description: Build the basic message model before moving to multiplexing and framing.

#### 9.2 HTTP/2 framing and multiplexing
Short description: Show how streams, frames, HPACK, and connection reuse affect both efficiency and fingerprinting.

#### 9.3 HTTP/3 over QUIC
Short description: Tie the application protocol to its UDP-based transport foundation.

### 10. TLS, certificates, and trust
Short description: Build the cryptographic literacy needed to understand modern proxy camouflage and secure tunneling.

#### 10.1 What TLS protects
Short description: Explain confidentiality, integrity, peer authentication, and why they matter to proxies and censors alike.

#### 10.2 The TLS handshake
Short description: Walk through ClientHello, ServerHello, key agreement, certificates, and ALPN at a high level.

#### 10.3 SNI, ALPN, and certificate metadata
Short description: Show which pieces are visible and why they are important for classification and blocking.

#### 10.4 ECH and the future of hiding more handshake metadata
Short description: Introduce Encrypted ClientHello as an evolution of TLS privacy.

## Part V — Deep packet inspection and censorship mechanics
Short description: Explain how networks classify and interfere with traffic so the reader understands what a circumvention system is reacting to.

### 11. What DPI really is
Short description: Define DPI as traffic classification using packet contents, metadata, timing, and behavioral signals.

#### 11.1 Payload inspection
Short description: Explain signature matching, protocol decoding, and pattern recognition in simple terms.

#### 11.2 Metadata inspection
Short description: Show how IPs, ports, SNI, ALPN, DNS, packet sizes, and timing can be enough even when payloads are encrypted.

#### 11.3 Behavioral inspection
Short description: Introduce traffic analysis, burst shapes, retry patterns, and active probing as higher-level detection methods.

### 12. Common censorship actions
Short description: Show what happens after traffic is identified.

#### 12.1 Blocking and dropping
Short description: Explain silent drops, explicit resets, and route blackholes.

#### 12.2 Throttling and quality degradation
Short description: Show how a censor can make a protocol unusable without fully blocking it.

#### 12.3 DNS manipulation and domain control
Short description: Cover poisoned answers, NXDOMAIN tricks, and resolver-level interference.

#### 12.4 Active probing and confirmation attacks
Short description: Explain how a censor may connect back to a suspected server to verify its real behavior.

### 13. How circumvention systems respond
Short description: Present the general design patterns without turning the chapter into an abuse manual.

#### 13.1 Encryption
Short description: Hide payload meaning and protect integrity.

#### 13.2 Cover traffic and camouflage
Short description: Make traffic resemble something ordinary or less suspicious.

#### 13.3 Fragmentation, padding, and timing control
Short description: Show how shape and boundaries affect detectability.

#### 13.4 Protocol choice and fallback paths
Short description: Explain why resilient systems offer multiple transports and multiple failure-handling strategies.

## Part VI — Xray-core mental model
Short description: Move from general networking into the specific architecture Xray-core uses internally.

### 14. The Xray traffic pipeline
Short description: Explain the inbound → sniffing → dispatch → route → outbound → transport path that appears throughout the codebase.

#### 14.1 Inbounds
Short description: Teach that inbounds accept local or remote traffic and translate it into Xray’s internal processing flow.

#### 14.2 Dispatch and link objects
Short description: Explain how Xray connects readers and writers internally to move traffic between components.

#### 14.3 Routing and policy
Short description: Show how Xray decides where traffic should go and what limits or behaviors apply.

#### 14.4 Outbounds
Short description: Explain how traffic leaves Xray toward the destination or another proxy hop.

### 15. Reading the repository like a system diagram
Short description: Turn the directory tree into a mental map for future contributors.

#### 15.1 `core/` and `main/`
Short description: Cover startup, lifecycle, versioning, config loading, and the executable entry path.

#### 15.2 `app/`
Short description: Cover higher-level features such as dispatcher, router, DNS, policy, stats, and observability.

#### 15.3 `proxy/`
Short description: Cover the inbound and outbound protocol implementations, including where protocol behavior actually lives.

#### 15.4 `transport/`
Short description: Cover the network transport implementations and lower-level movement of bytes and packets.

#### 15.5 `common/` and `features/`
Short description: Cover shared utilities, interfaces, buffers, sessions, and abstractions that many modules depend on.

#### 15.6 `infra/conf/`
Short description: Cover how JSON, YAML, and TOML configuration turns into internal protobuf-backed structures.

## Part VII — Xray protocols and what each one teaches
Short description: Use each supported protocol family to teach a design lesson, not just a configuration recipe.

### 16. SOCKS and HTTP proxies
Short description: Start with the simplest proxy concepts before moving to Xray-native or advanced protocols.

#### 16.1 Why classic proxies still matter
Short description: Explain local app integration, debugging convenience, and baseline traffic flow understanding.

#### 16.2 Their limits under modern censorship
Short description: Show why plain proxies are easy to identify and insufficient by themselves.

### 17. Shadowsocks
Short description: Present Shadowsocks as a historical and practical stepping stone in modern circumvention design.

#### 17.1 Basic framing and encryption ideas
Short description: Explain the core simplicity that made Shadowsocks influential.

#### 17.2 What it does well and where it struggles
Short description: Discuss deployment ease, performance, and fingerprint-resistance trade-offs.

### 18. VMess
Short description: Explain VMess as an older Xray/V2Ray-family design that is still useful for architectural understanding.

#### 18.1 Identity, framing, and message design
Short description: Show how VMess packages traffic and authenticates peers.

#### 18.2 Why history matters
Short description: Use VMess to teach protocol evolution and why newer approaches emerged.

### 19. VLESS
Short description: Present VLESS as a lighter design that separates concerns and works well with modern transport/security combinations.

#### 19.1 Why “less” matters
Short description: Explain the benefit of a leaner protocol core with externalized security layers.

#### 19.2 VLESS as a building block
Short description: Show why VLESS is often paired with TLS, XTLS, or REALITY rather than trying to do everything itself.

### 20. Trojan
Short description: Explain Trojan as a design that leans heavily on looking like ordinary TLS-wrapped traffic.

#### 20.1 The camouflage idea
Short description: Show the intuition behind making traffic resemble common HTTPS behavior.

#### 20.2 Operational strengths and weaknesses
Short description: Discuss why resemblance helps, and where fingerprinting pressure still exists.

### 21. WireGuard, TUN, and full-device tunneling
Short description: Expand the reader’s view from per-app proxying to system-wide packet capture and forwarding.

#### 21.1 TUN interfaces
Short description: Explain virtual network interfaces and why they let software route device traffic.

#### 21.2 WireGuard concepts
Short description: Cover keys, peers, tunnels, and packet-oriented VPN design at a beginner level.

#### 21.3 When packet tunnels beat app-layer proxies
Short description: Compare simplicity, control, compatibility, and visibility trade-offs.

## Part VIII — Xray transports and carriers
Short description: Show how the same logical proxy protocol can ride on different underlying transports.

### 22. Raw TCP and UDP carriers
Short description: Explain the simplest carriers first so more complex transports feel like variations, not magic.

#### 22.1 Direct TCP carriage
Short description: Show when a protocol over plain TCP is simple and when it becomes easy to fingerprint.

#### 22.2 Direct UDP carriage
Short description: Explain where datagram-style carriers shine and where networks punish them.

### 23. WebSocket, gRPC, and HTTP-based carriers
Short description: Explain how Xray rides on web-shaped transports to fit into common traffic patterns.

#### 23.1 WebSocket
Short description: Show how an HTTP upgrade can become a long-lived bidirectional channel.

#### 23.2 gRPC over HTTP/2
Short description: Explain why framed RPC traffic can act as a carrier and how it inherits HTTP/2 behavior.

#### 23.3 HTTP Upgrade and SplitHTTP
Short description: Explain the middle ground between raw tunnels and full RPC-based transports.

### 24. KCP, Hysteria, and QUIC-style performance thinking
Short description: Compare transports designed to perform well under loss, delay, or unstable networks.

#### 24.1 Why “faster” often means “more adaptive”
Short description: Show that performance comes from recovery behavior, congestion control, and path tolerance, not just raw speed.

#### 24.2 Congestion and reliability choices
Short description: Explain the design trade-offs each transport makes.

#### 24.3 Detectability versus performance
Short description: Teach that the best-performing transport is not always the safest under a censor.

## Part IX — TLS, uTLS, XTLS, and REALITY in Xray
Short description: Focus on the security and fingerprint-resistance layers that make Xray distinctive.

### 25. Standard TLS inside Xray
Short description: Explain how Xray uses conventional TLS as both a security layer and a camouflage layer.

#### 25.1 Certificates and server identity
Short description: Show how normal TLS trust works before explaining advanced variants.

#### 25.2 ALPN, SNI, and handshake shape
Short description: Explain which handshake details help or hurt believable traffic appearance.

### 26. uTLS and fingerprint control
Short description: Explain why a client may want to imitate real-world TLS stacks instead of sending a unique fingerprint.

#### 26.1 What a TLS fingerprint is
Short description: Introduce JA3-style thinking without drowning the learner in details too early.

#### 26.2 Why imitation matters
Short description: Show how looking like a browser or common client can reduce classification risk.

### 27. XTLS and Vision
Short description: Explain the XTLS idea of optimizing encrypted traffic handling while keeping the reader grounded in actual traffic flow.

#### 27.1 Why XTLS exists
Short description: Present the performance and processing motivations behind XTLS-related designs.

#### 27.2 Vision as traffic-state-aware handling
Short description: Explain that Vision tracks TLS-like flow state to decide when to pad, unwrap, or switch handling modes.

#### 27.3 Performance, padding, and observability trade-offs
Short description: Show that optimization and camouflage decisions interact with each other.

### 28. REALITY
Short description: Present REALITY as one of the key modern ideas in the Xray ecosystem and place it in the broader anti-censorship landscape.

#### 28.1 The core design intuition
Short description: Explain the high-level idea of borrowing believable TLS appearance while enforcing private server-side acceptance.

#### 28.2 Why REALITY changed deployments
Short description: Show why it reduced some operational burdens compared with traditional public-certificate setups.

#### 28.3 Threat model and limits
Short description: Clarify that no single transport/security stack defeats every adversary or every deployment mistake.

## Part X — Sniffing, routing, DNS, and decision-making inside Xray
Short description: Explain how Xray recognizes traffic and decides what to do with it.

### 29. Traffic sniffing in Xray
Short description: Show how Xray can inspect early bytes and metadata to infer protocol and domain information.

#### 29.1 HTTP sniffing
Short description: Explain how host and request structure can reveal intended destinations.

#### 29.2 TLS sniffing and SNI extraction
Short description: Explain how the early TLS handshake reveals domain intent before application payloads flow.

#### 29.3 QUIC sniffing
Short description: Show that UDP-based protocols still expose identifiable structure during setup.

#### 29.4 FakeDNS-assisted inference
Short description: Explain how DNS strategy can feed routing and domain recovery inside the engine.

### 30. Routing logic
Short description: Show that routing is not only about geography but also about protocol class, domain type, policy, and operational goals.

#### 30.1 Domain-based routing
Short description: Explain when domains are available and why they are often more useful than raw IPs.

#### 30.2 IP and geo-based routing
Short description: Cover geoIP, direct routes, block routes, and regional policy decisions.

#### 30.3 Rule ordering and policy design
Short description: Teach how routing becomes a readable, maintainable system instead of a pile of exceptions.

### 31. DNS inside Xray
Short description: Connect resolution strategy directly to performance, censorship resistance, and routing quality.

#### 31.1 Built-in DNS behavior
Short description: Explain why many Xray deployments need DNS decisions inside the engine, not outside it.

#### 31.2 FakeDNS
Short description: Show how synthetic answers can preserve domain context for later routing decisions.

#### 31.3 DNS as both a feature and an attack surface
Short description: Teach the reader to think of DNS choices as architecture, not mere setup detail.

## Part XI — Configuration as architecture
Short description: Teach readers to read an Xray config as a design diagram rather than a random JSON blob.

### 32. How to read an Xray config
Short description: Break a config into inbounds, outbounds, routing, DNS, transport, and policy sections.

#### 32.1 Minimal config
Short description: Define the smallest useful setup and what each required field means.

#### 32.2 Multi-outbound config
Short description: Explain how one inbound can feed several egress choices based on rules.

#### 32.3 Layered config thinking
Short description: Show how protocol, transport, and security are separate layers composed together.

### 33. Configuration mistakes beginners make
Short description: Turn common confusion points into teachable lessons.

#### 33.1 Mixing protocol and transport concepts
Short description: Explain why VLESS is not the same thing as WebSocket, TLS, or REALITY.

#### 33.2 Forgetting DNS and routing interactions
Short description: Show how bad DNS choices can sabotage otherwise good transport choices.

#### 33.3 Chasing “best” settings without a threat model
Short description: Teach that good design is context-specific and depends on network conditions and censor behavior.

## Part XII — Performance, reliability, and operational trade-offs
Short description: Help the reader think like an engineer who balances stealth, speed, simplicity, and maintainability.

### 34. Throughput, latency, and CPU cost
Short description: Explain why cryptography, multiplexing, buffering, and user-space processing all have a price.

#### 34.1 Buffering and copy paths
Short description: Connect code-level buffer flow to real-world performance outcomes.

#### 34.2 Handshakes and setup cost
Short description: Show why connection establishment matters as much as steady-state throughput.

#### 34.3 Mobile, satellite, and lossy-network considerations
Short description: Teach how poor networks change the “best” design choice.

### 35. Failure modes and debugging mindset
Short description: Teach the learner how to reason when a deployment fails without blindly changing random settings.

#### 35.1 DNS failures
Short description: Show how bad resolution produces symptoms that look like transport or routing problems.

#### 35.2 TLS and certificate failures
Short description: Explain the most common trust and handshake mismatches.

#### 35.3 Transport mismatch and path blocking
Short description: Show how a chosen carrier can fail because of path policy, MTU, or middlebox behavior.

## Part XIII — Learning to read and contribute to Xray-core
Short description: Turn the learner from a user into a reader of the codebase and then into a contributor.

### 36. Where traffic enters the codebase
Short description: Start from startup, config loading, feature registration, and the main runtime path.

#### 36.1 Startup path
Short description: Follow `main/` into `core/` so the reader sees how configuration becomes a running server.

#### 36.2 Feature registration
Short description: Show how imports and registration patterns wire protocols and transports into the binary.

### 37. How to trace one request through Xray
Short description: Give the reader a repeatable code-reading method.

#### 37.1 From inbound accept to dispatcher
Short description: Follow a connection from the edge into the internal handoff path.

#### 37.2 From sniffing to routing
Short description: Show where protocol/domain inference influences decisions.

#### 37.3 From outbound to transport
Short description: Show where logical proxy behavior meets network carriage.

### 38. How protocols are added
Short description: Explain the interface and registration patterns a contributor needs to understand first.

#### 38.1 Inbound and outbound interfaces
Short description: Show the small core contracts that define protocol behavior inside Xray.

#### 38.2 Config structures and protobuf-backed definitions
Short description: Explain how protocol-specific configuration reaches runtime code.

#### 38.3 Tests, examples, and safe extension points
Short description: Teach where to look before adding a new idea or changing an existing one.

### 39. How transports are added
Short description: Explain how new carriers fit into the engine separately from higher-level protocol logic.

#### 39.1 Listener and dialer concepts
Short description: Show the two ends of a transport integration.

#### 39.2 Reusing common abstractions
Short description: Explain how buffers, session context, and routing metadata reduce repeated work.

### 40. How to become a useful contributor
Short description: Give the reader a realistic on-ramp from beginner to meaningful pull requests.

#### 40.1 Start by reading existing protocol folders
Short description: Learn patterns by comparing simpler protocols with more advanced ones.

#### 40.2 Fix documentation and tests first
Short description: Build confidence and context before touching tricky transport or cryptographic logic.

#### 40.3 Move from bug fixes to feature design
Short description: Teach a gradual path toward proposing or implementing larger changes.

## Part XIV — Designing your own unique system
Short description: End with systems thinking so the reader can combine ideas instead of only copying existing recipes.

### 41. Thinking in layers instead of brands
Short description: Teach the reader to choose protocol, transport, DNS, routing, and fingerprint strategy as separate decisions.

#### 41.1 Pick the threat model first
Short description: Decide what the censor can see, block, or probe before choosing any stack.

#### 41.2 Pick the carrier next
Short description: Choose what kind of path behavior the network will tolerate.

#### 41.3 Pick observability and maintainability limits
Short description: Balance stealth goals against operability, debugging, and long-term maintenance.

### 42. What makes a design genuinely “unique”
Short description: Explain that uniqueness comes from thoughtful composition and clear trade-offs, not novelty for its own sake.

#### 42.1 New combinations
Short description: Show how combining known building blocks in a better way can still be valuable.

#### 42.2 New control logic
Short description: Explain how smarter routing, fallback, and adaptation can matter as much as inventing a new wire format.

#### 42.3 New operational assumptions
Short description: Show that a system built for one censor, one device class, or one traffic profile may deserve different design choices.

## Part XV — Appendices
Short description: Finish with fast-reference material that makes the future book practical and reusable.

### 43. Glossary
Short description: Define packets, flows, SNI, ALPN, QUIC, DPI, NAT, MTU, multiplexing, and other recurring terms in one place.

### 44. Xray-core code map
Short description: Provide a one-page directory-to-responsibility map for fast orientation during code reading.

### 45. Suggested learning path
Short description: Offer several reading orders such as “absolute beginner,” “network engineer,” “operator,” and “future contributor.”

### 46. Suggested labs for the future full book
Short description: List safe learning exercises such as packet capture observation, TLS handshake decoding, config tracing, and code-flow walkthroughs.
