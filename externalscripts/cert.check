#!/usr/bin/env python3

# AUTHOR:  Roman Bergman <roman.bergman@protonmail.com>
# LICENSE: GNU AGPL-3.0
# VERSION: 0.2.2

# STL
import sys
import ssl
import socket
import datetime


class CertCheck(object):
    def get_certificate(self, host, port):
        cert_context = ssl.create_default_context()
        try:
            with socket.create_connection((host, port)) as socket_host:
                with cert_context.wrap_socket(socket_host, server_hostname=host) as socket_ssl:
                     return socket_ssl.getpeercert()['notAfter']
        except Exception as err:
            return False

    def days_before_expiration(self, host, port):
        if host and port:
            dbe = self.get_certificate(host, port)
            if dbe:
                expire_date = datetime.datetime.strptime(dbe, '%b %d %H:%M:%S %Y %Z')
                day_to_expiration = expire_date - datetime.datetime.now()
                print(day_to_expiration.days)
            else: print(-1)
        else: print(-1)



# MAIN
if __name__ == '__main__':
    CertCheck().days_before_expiration(host=sys.argv[1], port=sys.argv[2])