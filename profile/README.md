# Leo Development(Draft)
### 1. Concept
**What’s the difference between Leo and Solidity?**  
Using Record Types to store private data on the chain. ( Solidity use Account model)
Leo compiles code into an AVM (Aleo Virtual Machine) code format that is conducive to generating zero-knowledge proof circuits.  

**What’s the relationship between Transition and Finalize?**  
Each Transition could have a option related Finalize scope.  
Transition is executed locally and generates proof then verified on the chain.  
The Finalize is executed on the chain after the related Transition is verified, we can store the data on the chain publicly.  
Gas calculation  
Base Fee  
Fixed execution gas  
Finalize operation fee  
Priority Fee  
Test Framework

### 2. Common Usage
**How to deploy a program on the Aleo?**  
Use snarkos   
Use aleo.tools  

**How to execute a program function on the Aleo?**  
Transfer privately  
Transfer publicly  

### 3. Advanced Types
String Type: Not supported yet, but we could use `u128` to represent 4 letters.   
Array Type  
Tuple Type  

### 4. Learn from Examples
Token Example  
Order book Example  
Swap Example  
CrossBridge Example  


## Aleo and Leo Development FAQ (Draft 2)

### 1. Development and Programming
**Handling Multiple Record Types**  
Q: When will multiple record types be supported?  
A: Multiple records are supported now.  

**Error Handling and Record Interactions**  
Q: Can errors be thrown to prevent transaction validation?  
A: Direct error throwing is not supported. Implement safety checks and avoid   modifying records on failure. Note that the command leo build doesn't generate errors like underflows.  

**Combining Records and Trust Issues**  
Q: How to handle combining records from multiple addresses and trust issues?  
A: Design functions for each role and mitigate trust issues with callable functions by any past bidder.  

**Trustless Swaps**  
Q: Is it possible to implement trustless swaps in Aleo?  
A: Yes. A future example by Howard Wu will demonstrate this.  

**Regulated Financial Market Workflows**   
Q: How to model a propose-accept/reject workflow in Leo?  
A: Implement a system where transfers require mutual approval.  

**Testing Framework**  
Q: Does Leo come with a testing framework for smart contracts before deployment?  
A: Explore https://github.com/leology-org/leology. The Aleo team is developing a dedicated framework.  

### 2. Language and Syntax  
**Aleo Operations**  
Q: What operations are available in Aleo?  
A: Increment and decrement operations are no longer available. Leo supports fully mapping operations: https://github.com/AleoHQ/snarkVM/blob/v0.16.15/synthesizer/program/src/logic/finalize_operation/mod.rs#L24  

**Syntax Features**  
Q: Can tuple types be declared outside function/transition return types in Leo?  
A: Currently, tuple types are limited to function/transition return types.  

**String Type**  
Q: Does Leo-lang support the “string” type?    
A: Use struct and convert dec to string. Refer to https://github.com/demox-labs/art-factory for examples in creating NFTs and dealing with string data.  

### 3. IDE and Tooling
**Plugin and Version Identification** 
Q: Is there an IntelliJ plugin for Leo/Aleo development?  
A: Ongoing efforts exist for an IntelliJ plugin: https://plugins.jetbrains.com/plugin/19979-leo  

**GitHub Copilot Utility**
Q: How can GitHub Copilot assist in Aleo development?  
A: Copilot suggests patterns in Leo and Aleo and provides common implementations.  

### 4. Deployment and Operations
**Deployment Issues**  
Q: What should I do if I face issues deploying my contract?  
A: Check for updates on the Slingshot repository and separate imports into different programs.  

**Memory and Technical Issues**  
Q: How to address memory issues with the dev beacon node?  
A: Use jemalloc as a workaround and pre-allocate Vecs for known sizes.  

### 5. Community and Resources
**Feedback and Updates**  
Q: How can I stay informed about Aleo development?  
A: Watch repositories on GitHub, join Aleo Devs/Aleo Events Telegram channel, follow Aleo X on Twitter, and join Aleo Discord.  

**Learning Resources**  
Q: How can I improve my understanding of Rust for Aleo's core libraries?  
A: Read the Rust book and participate in GitHub discussions and development groups. A beginner's resource for understanding ZK and underlying protocols for Aleo is https://github.com/ZKCamp/aleo-course.  

### 6. SDK and API Usage
**SDK and API Concerns**  
Q: What could cause HTTP errors during domain deployment?  
A: Check reverse proxy configuration and direct IP connections. Alternative API options include: https://api.explorer.aleo.org/v1/testnet3/, https://explorer.hamp.app/testnet3/.  

**Execution and Troubleshooting**  
Q: Why might there be a slowdown in execution when using the SDK?  
A: Wasm is pre-compiled. Consider enabling multi-threading to improve speed.  

### 7. Advanced Topics and Community Discussions
**Advanced Programming**  
Q: Are there examples for using arrays in Aleo?  
A: Yes, see the "zk_texas_holdem" repository for examples.  

**Community Topics**  
Q: What recent discussions have been raised in the community?  
A: Topics include ARC0721, composability, NFT standards, and on-chain images. More at: https://github.com/AleoHQ/ARCs/discussions  

### 8. Troubleshooting and Error Handling
**Runtime Error in Aleo Wasm File**  
Q: How to address a runtime error in the Aleo Wasm file?  
A: Check node status, SDK usage, and recent changes impacting execution.
Comments added by team members:  
Reminder: The command leo build doesn't generate errors like underflows. Execution and testing are essential for identifying potential issues.  
AleoSwap reference: https://github.com/AleoswapFinance/AleoSwap  
PrivX Exchange Contract: https://github.com/privx-exchange/privx-exchange-contract/blob/develop/src/main.leo  
For node status, visit https://status.aleo.org  

## Aleo and Leo Development FAQ (Draft 1)
### Development and Programming 
**1. Handling Multiple Record Types**  
Q: When will multiple record types be supported?  
A: Support is planned. Currently, combine state into a single larger record and use pass throughs for functions.  

**2. Error Handling and Record Interactions**  
Q: Can errors be thrown to prevent transaction validation?  
A: Direct error throwing is not supported. Implement safety checks and avoid modifying records on failure.  
Even the command: `leo build` doesn't generate errors, such as underflows, in its output. It's essential to perform execution and testing to identify potential issues.

**3. Combining Records and Trust Issues**    
Q: How to handle combining records from multiple addresses and trust issues?  
A: Design functions for each role. Mitigate trust issues with callable functions by any past bidder.   

**4. Trustless Swaps**  
Q: Is it possible to implement trustless swaps in Aleo?  
A: Yes. A future example by Howard Wu will demonstrate this. You can try:  
AleoSwap:https://github.com/AleoswapFinance/AleoSwap  
PrivX: https://github.com/privx-exchange/privx-exchange-contract/blob/develop/src/main.leo  

**5. Regulated Financial Market Workflows**  
Q: How to model a propose-accept/reject workflow in Leo?  
A: Implement a system where transfers require mutual approval. Specific models can be designed within Leo.  

**6. Testing framework**  
Q: Does Leo come with a testing framework for smart contracts before deployment?  
A: Currently, you can explore https://github.com/leology-org/leology. Additionally, the Aleo team is actively developing a dedicated testing framework.  

### Language and Syntax
**1. Aleo Operations**  
Q: What operations are available in Aleo?  
A: Increment and decrement operations are no longer available. Leo has already supported fully mapping operations now, check for the details:
https://github.com/AleoHQ/snarkVM/blob/v0.16.15/synthesizer/program/src/logic/finalize_operation/mod.rs#L24

**2. Syntax Features**  
Q: Can tuple types be declared outside function/transition return types in Leo?  
A: Currently, tuple types are limited to function/transition return types.  

**3. String Type**  
Q: Does Leo-lang support the “string” type?  
A: Currently, you can use struct and convert dec to string. You can see how to do that with this repo https://github.com/demox-labs/art-factory. It shows how to create an NFT on Aleo and in the process, deal with string data.  

## IDE and Tooling
**1. Plugin and Version Identification**  
Q: Is there an IntelliJ plugin for Leo/Aleo development?  
A: Ongoing efforts exist to create an IntelliJ plugin. You can check this link:
https://plugins.jetbrains.com/plugin/19979-leo  

**2. GitHub Copilot Utility**  
Q: How can GitHub Copilot assist in Aleo development?  
A: Copilot suggests patterns in Leo and Aleo, assists with tasks, and provides common implementations.  

## Deployment and Operations
**1. Deployment Issues**  
Q: What should I do if I face issues deploying my contract?  
A: Check for updates on the Slingshot repository and separate imports into different programs.  

## Testing and Troubleshooting
**1. Memory and Technical Issues**  
Q: How to address memory issues with the dev beacon node?  
A: Use jemalloc as a workaround and pre-allocate Vecs for known sizes.  

## Feedback and Updates
**1. Feedback Channels**  
Q: How can I stay informed about Aleo development?  
A: Watch repositories on GitHub and join the Aleo Devs/ Aleo Events Telegram channel. You also follow Aleo X( Twitter) and Aleo Discord to stay up to date.  

**2. Real-Time Updates**  
Q: How can I receive real-time updates on Aleo development?  
A: Use the Watch feature on GitHub for repositories like ARCs, aleo, leo, etc.
Contributions and Community Involvement  

**3. Community Contributions**  
Q: Can I contribute to the Leo Learners group?  
A: Yes, participate in programming sessions and provide feedback on materials. You can join and help other learners in Aleo Devs channel Telegram or Aleo Discord channel. You also learn lots of things in that.  

**4. Learning Resources**  
Q: How can I improve my understanding of Rust for Aleo's core libraries?  
A: Read the Rust book and participate in GitHub discussions and development groups.  


## SDK and API Usage
**1. SDK and API Concerns**  
Q: What could cause HTTP errors during domain deployment?  
A: Check reverse proxy configuration and direct IP connections. The API provided by Aleo is not very stable, some other choices:  
https://api.explorer.aleo.org/v1/testnet3/  
https://explorer.hamp.app/testnet3/  

**2. Execution and Troubleshooting**  
Q: Why might there be a slowdown in execution when using the SDK?  
A: Wasm is pre-compiled. Consider enabling multi-threading to improve speed.  

## Advanced Topics and Community Discussions
**1. Advanced Programming**  
Q: Are there examples for using arrays in Aleo?  
A: Yes, see the "zk_texas_holdem" repository for examples.  

**2. Community Topics**  
Q: What recent discussions have been raised in the community?  
A: Topics include ARC0721, composability, NFT standards, and on-chain images. You can check the link: https://github.com/AleoHQ/ARCs/discussions  

## Python SDK Type Hinting Stubs
**1. SDK Usage Clarifications**  
Q: Are all functions accessible from Python in the SDK?  
A: Yes, all functions from py methods in the Python SDK are intended to be accessible.

**2. Troubleshooting and Error Handling**  
Q: How to address a runtime error in the Aleo Wasm file?  
A: Check node status, SDK usage, and recent changes impacting execution.  For node status, https://status.aleo.org  



