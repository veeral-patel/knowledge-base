# CH1 - What is security engineering?

From "Security Engineering" by Ross Anderson

## Good security engineering has 4 parts

- policy: our goals
- mechanisms: tools like tamper proof hardware, access control, etc used to enforce policy
- assurance: how much faith you can place on each mechanism
- incentive: the incentive that both defenders and attackers have to attack/defend

## Attack surfaces of everyday systems

### Banks

1. book-keeping system at each branch
2. ATMs
3. website
4. messaging systems with other banks
5. physical security of branches

### Military base

1. preventing radar from being jammed
2. hard-to-detect radio links
3. organizing secret information
4. protecting nuclear weapons

### Hospital

1. enforce policies on what staff can see what patient information
2. anonymizing patient data for research
3. display life-critical data in web/mobile/etc apps but prevent it from being changed
4. protect Internet-connected medical devices

### Home

1. electronic banking
2. authentication in car keys
3. authentication in mobile phones to carrier networks
4. DRM in consumer goods
5. house locks
6. electric meters
