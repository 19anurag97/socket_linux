Socket program on Linux m/c.(//for Windows winsock library.)
The ss command is used to dump socket statistics.
# ss -tulpn

Two types of Client To Send messages :

1)Connection initiation request.
    -> connect() client side.
    -> accept() server side.

2)Service request messages.
    client:
    -> sendto()
    -> sendmsg()
    Server:
    -> recvfrom()
    -> recvmsg()

____
// IPv4 AF_INET sockets:
struct sockaddr_in {
    short            sin_family;   // e.g. AF_INET, AF_INET6
    unsigned short   sin_port;     // e.g. htons(3490)
    struct in_addr   sin_addr;     // see struct in_addr, below
    char             sin_zero[8];  // zero this if you want to
};

struct in_addr {
    unsigned long s_addr;          // load with inet_pton()
};

struct sockaddr {
    unsigned short    sa_family;    // address family, AF_xxx
    char              sa_data[14];  // 14 bytes of protocol address
};
______
int com_sock_fd = accept( master_sock_tcp_fd, 
                ( struct sockaddr *)&client_addr, 
                &addr_len)

Monitor all clients activity at same time using select()
Linux maintain inbuilt data structure to maintain the set of
sockets file descriptor. "fd_set"
select system call monitors all socket fd's present in "fd_set"
