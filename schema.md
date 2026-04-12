This is where I will organize all of my current (non-deprecated) packages, as well as links to all of their wiki pages where you can get to everywhere else (their GitHub, NuGet, and read their documentation). 

Items that have links are for the repository that holds it and everything beneath it. 

## CSharp

- HowlDev.Web
    - [.Authentication](https://github.com/Cody-Howell/HowlDev.Web.Authentication)
        - .AccountAuth
            - Is my current AccountAuthenticator library. I believe it will just be my AuthService stuff.
        - .Middleware
            - Is my current IdentityMiddleware function. I think I should export just the functions it needs as an interface, and anything that implements that interface (such as my AuthService) will enable it to work. This would also let me expand into more types that do the same thing, such as my EmailAuthenticator (RIP, we never knew ye).
    - .OpenAI (Not yet started)
        - Includes all of the services I need to effectively talk with a client that implements the OpenAI spec. I want functions/services that do the following:
            - Send A Message
                - Takes in a list of messages, functions, and an optional System prompt and returns the AI response from it. One and done, no loops. 
            - Agentic Loop
                Given a few parameters (maybe a configuration object, maybe some static fields), create a loop that runs until its done or the configuration stops it. 
        - Both of the above should be available as Responses and as Streams. I'd like to experiment with both. 
        - I'd want my own Function definitions so that I can more easily integrate with it; for example, I don't need to read the AI output and check which function to run in my loop, I'll define an interface and make _it_ do that. 
    - [.Helpers](https://github.com/Cody-Howell/HowlDev.Web.Helpers)
        - .WebSockets
            - Has a WebSocketService to simplify registration and sending of messages over WebSockets.
        - .DbConnector
            - My little helper class that I use basically everywhere. Uses Dapper to correctly pool threads and properly multithread calls. 
            
- [HowlDev.Data](https://github.com/Cody-Howell/HowlDev.Data)
    - .Structures
        - Includes a Graph and Circuit class
    - .Algorithms
        - Depends on Structures. Completes a few different traversals using WhateverFirstSearch. 
        - Should also include a few default tiny interfaces that I can do arbitrary algorithms to. I have one for DependencyChecking which checks IEquatable, which would be nice to have here. 
    - .Probability
        - .Sampling
            - Inlcudes things like a deck of cards, coin, n dice roll, and hopefully an arbitrary one that you can pack with data types that (maybe) fit a specific interface, then you can perform With and Without Replacement on them. Pretty easy. 

- HowlDev.Simulation
    - [.Physics](https://github.com/Cody-Howell/HowlDev.Simulation.Physics)
        - .Primitive2D
            - Contains all the classes I've already built for Rotations, Points, Lines, Equations, etc. 
        - .Grid2D (In progress)
            - Depends on the Primitive library above.
            - Enables you to generate a grid of either squares or hexagons (or triangles..) with a number of helper methods. From each node, you can specify whether or not you can reach all of your neighbor nodes, and I should implement A* search (using the Algorithms library) to do pathfinding on both of those libraries.  

- HowlDev.IO
    - [.Text](https://github.com/Cody-Howell/HowlDev.IO.Text)
        - .Parsers
            - Includes a few different parsings of different files. Includes the Enum and value type I already have implemented for the ConfigFile section.
        - .ConfigFile
            - Is my current ConfigFileLibrary. Depends on the Parsers in the part above. 
    - [.Binary](https://github.com/Cody-Howell/HowlDev.IO.Binary) (In progress)
        - .Encoding
            - Takes in arbitrary objects, and through an algorithm, determines a semi-optimal binary encoding that sends the minimal amount of data. 
        - .Decoding
            - Taking in a bit stream and a class definition, creates the object requested. 
    - .OOSql (Ideating)
        - Something I used to think was called DapperWrapper, but Object-Oriented SQL is exactly what I'm trying to design. 
        - Can take in SQL files and parse them into classes with Source Generators.
            - From there, creates objects that combine together to create queries. This includes simple DTO getters up to logical branches off of existing queries.
        - Includes a static function at runtime to validate given objects against the database to check for errors.
        - May also include static linting to prevent some of those errors, such as mismatched names.
            - I'm thinking this is like if a DTO has an "Id" field and you're joining two tables together, you need to specify which table you want the id of through attributes.

- [HowlDev.AI](https://github.com/Cody-Howell/HowlDev.AI)
    - .Core
        - Contains all the interfaces for classes and algorithms within (and without) this namespace. (Without means interfaces for external objects to implement for some algorithmic things)
    - .Structures
        - Contains (for now, only) the Neural Network class. This is a naive implementation with two-dimensional neurons and weights arranged in layers. 
    - .Training
        - .Genetic
            - Holds a class (and calls the interface from Core) to run a genetic algorithm. Holds a few parameters and option classes for defining the actions of the algorithm.  

- [HowlDev.Quality](https://github.com/Cody-Howell/HowlDev.Quality) (Ideating)
    - .TestGeneration
        - Takes in class types and configurations and generates test files that do some action. Some are full enumerations; given these three different enums, make tests for all different combinations. Some capture the current value of the system; given method and boundaries, make tests that test what the system currently returns. Some can help you fill out test coverage by checking branching paths. 
    - .Performance
        - Helps generate functions/low cast parameter definitions for performance analysis. 
    - .Mutations
        - Implements some different types of mutation tests on your classes, and determines where your tests don't catch a mutation. 

- [HowlDev.Cli](https://github.com/Cody-Howell/HowlDev.Cli)
    - .TextDTO
        - CLI tool that takes in a file or folder of JSON files that export to C#, TS, and Zod types in other folder (overwriting if they currently exist). This is designed to make DTO objects easier to maintain in a full stack project. 
    - FullStackBuilder (In progress)
        - CLI tool that uses the Vite builder and Dotnet solution builder to bootstrap small full-stack apps. 
        - Has options to install default packages for JS (such as Zod, React Router, and perhaps some custom ones) and for C# (primarily my own packages that I use). 
            - For packages that have setup (or for other setup options like Vite building into an external folder), have parameters to set them up by default. This applies mainly to my personal libraries that have a small amount of setup. 
        - Also can generate Docker Composes/Dockerfiles. 

- [HowlDev.CodeGen](https://github.com/Cody-Howell/HowlDev.CodeGen) (This is currently on hiatus)
    - .Core
        - Holds any core object definitions used inside these objects to build the required files. 
    - .CSharp
        - Holds all the methods to generate C# code based off of configuration files. 
    - .TypeScript
        - Holds all the methods to generate TS code based off of configuration files. 

- HowlDev.Core
    - Empty


## JavaScript

I've also published some NPM libraries to consolidate some ideas on the frontend. These include a different format (published as @howldev/library-name) and saved as a different repository name to differentiate from C# libraries (howldev.library-name). 

- [howldev.extendable-md](https://github.com/HowlDevOrg/howldev.extendable-md)
    - Provides a logical default as a markdown parser, LaTeX, Code, and Mermaid viewer. 
        - Also includes some extra features, such as an expandable element to hide an amount of text for easier reading
    - Provides extension methods to add or override new items in the code viewer or Markdown parsing, given a few arguments 

- howldev.display (Ideating)
    - Provides a bunch of smaller components such as the Collapsible Header and the Code Display

- howldev.binary (Ideating)
    - I believe that I can use Zod objects to reflect off of to make the frontend half of my C# Binary Encoder as a library instead of as generated code (though I may still inspect to generate code for high performance). 

- howldev.sockets (Ideating)
    - Make my own custom socket handler to learn how it works, which automatically handles connections, reconnection, and possible a function to query data on load. 
    - I'm considering extending this to a C# library as well where I mimic the function of Phoenix Channels (multiple things moving through a single socket connection) since.. that seems fairly straightforward? 