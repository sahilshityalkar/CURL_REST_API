# How to create a REST API with Express.js in Node.js

An Express application is most often used as a backend application in a client-server architecture whereas the client could be written in React.js or another popular frontend solution and the server could be written in Express. Both entities result in a client-server architecture (frontend and backend relationship) whereas the backend would be needed for (A) business logic that shouldn't be exposed as source code to the frontend application -- otherwise it would be accessible in the browser -- or for (B) establishing connections to third-party data sources (e.g. database(s)).

However, don't mistake client application always for frontend and server application always for backend here. These terms cannot be exchanged that easily. Whereas a frontend application is usually something seen in the browser, a backend usually performs business logic that shouldn't be exposed in a browser and often connects to a database as well.

`Frontend -> Backend -> Database`

But, in contrast, the terms client and server are a matter of perspective. A backend application (Backend 1) which consumes another backend application (Backend 2) becomes a client application (Backend 1) for the server application (Backend 2). However, the same backend application (Backend 1) is still the server for another client application which is the frontend application (Frontend).

`Frontend -> Backend 1 -> Backend 2 -> Database`

If you want to answer the client-server question if someone asks you what role an entity plays in a client-server architecture, always ask yourself who (server) is serving whom (client) and who (client) consumes whom's (backend) functionalities?

That's the theory behind client-server architectures and how to relate to them. Let's get more practical again. How do client and server applications communicate with each other? Over the years, there existed a few popular communication interfaces (APIs) between both entities. However, the most popular one is called REST defined in 2000 by Roy Fielding. It's an architecture that leverages the HTTP protocol to enable communication between a client and a server application. A server application that offers a REST API is also called a RESTful server. Servers that don't follow the REST architecture a 100% are rather called RESTish than RESTful. In the following, we are going to implement such REST API for our Express server application, but first let's get to know the tooling that enables us to interact with a REST API.

# CURL FOR REST APIS

If you haven't heard about cURL, this section gives you a short excursus about what's cURL and how to use it to interact with (REST) APIs. The definition taken from Wikipedia says: "cURL [...] is a computer software project providing a library and command-line tool for transferring data using various protocols." Since REST is an architecture that uses HTTP, a server that exposes a RESTful API can be consumed with cURL, because HTTP is one of the various protocols.

First, let's install it one the command line. For now, the installation guide is for MacOS users, but I guess by looking up "curl for windows" online, you will find the setup guide for your desired OS (e.g. Windows) too. In this guide, we will use Homebrew to install it. If you don't have Homebrew, install it with the following command on the command line:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

If you haven't heard about Homebrew, read more about it over here. Next, install cURL with Homebrew:

`brew install curl`

Now, start your Express server from the previous sections. Once your application is started, execute curl http://localhost:3000 in another command line window. Make sure the port matches your port and the Express server is running. After executing the command, you should see the "Hello World!" printed on the command line. Congratulations, you just have consumed your Express server as a client with something else than a browser.

`(Browser (Client) -> Express Server) = ( cURL (Client) -> Express Server)`

Whether you access your Express application on http://localhost:3000 in the browser or via the command line with cURL, you should see the same result. Both tools act as clients whereas the Express application is your server. You will see in the next sections how to use cURL to verify your Express application's REST API, that we are going to implement together, on the command line instead of in the browser.