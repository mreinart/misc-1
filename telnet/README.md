# telnet

## Documentation

* [telnet_connect](#telnet_connect)
* [telnet_disconnect](#telnet_disconnect)
* [telnet_send](#telnet_send)
* [telnet_receive](#telnet_receive)
* [Example](#example)

### telnet_connect
```c
int telnet_connect(const char* address, const unsigned port);
```
> Connect to a telnet server
* *RETURN (SUCCESS)* : Returns a socket to communicate with the server on.
* *RETURN (ERROR)* : Returns a negative value.
* *address* : URL of the server
* *port* : Telnet port of the server. Usually port 23

### telnet_disconnect
```c
void telnet_disconnect(int sockfd);
```
> Disconnect from telnet server
* *sockfd* : Socket used for communication with the telnet server

### telnet_send
```c
void telnet_send(int sockfd, const char* message);
```
> Send a message to the telnet server
* *sockfd* : Socket used for communication with the telnet server
* *message* : The string you would like to send to the server

### telnet_receive
```c
ssize_t telnet_receive(int sockfd, char* buffer, unsigned size);
```
> Receives a message from the telnet server.
* Blocks until a message has been received.
* *RETURN* : Returns the size of the received message or Null if the connection has been closed by the server

### Example
```c
/* Streams Star Wars Episode IV to your command line
 */

#include <stdio.h>
#include <telnet.h>

int main()
{
	int socket;
	char buffer[1024];

	socket = telnet_connect("towel.blinkenlights.nl", 23);
	if(socket < 0)
	{
		fprintf(stderr, "ERROR: Failed to connect to server!\n");
		return(-1);
	}

	while(telnet_receive(socket, buffer, 1024))
	{
		puts(buffer);
	}

	telnet_disconnect(socket);

	return(0);
}
```