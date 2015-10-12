# UPnP

The guhd server can be discovered in the local network by using the **UPnP 1.1** ([Universal Plug and Play](https://en.wikipedia.org/wiki/Universal_Plug_and_Play)) network discovery. The server will present it self as [UPnP Basic](http://upnp.org/specs/basic/basic1/) device according to the following specifications:

http://upnp.org/specs/basic/UPnP-basic-Basic-v1-Device.pdf

A detailed documentation of the UPnP device architecture can be found here: 

http://upnp.org/specs/arch/UPnP-arch-DeviceArchitecture-v1.1.pdf

# Discovering guh in the network

Once guhd is started it can be discovered over the [Simple Service Discovery Protocol](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol) (SSDP). A client can perform a discovery by binding to the UDP multicast address `239.255.255.250` on port `1900`.

In order to search for UPnP devices in the network a client can send following message to the UPD multicast socket:

    M-SEARCH * HTTP/1.1
    HOST:239.255.255.250:1900
    MAN:"ssdp:discover"
    MX:4
    ST: ssdp:all

> **Note:** use `\r\n` at the end of each line and twice at the end of the message.

Each UPnP device in the network will respond to this SSDP *M_SEARCH* search message with a HTTP message. The guhd server response will look like this:


    HTTP/1.1 200 OK
    Cache-Control: max-age=1900
    DATE: Mon, 12 Oct 2015 09:39:36 GMT
    EXT:
    CONTENT-LENGTH:0
    Location: http://10.10.10.50:3333/server.xml
    Server: guh/0.6.0 UPnP/1.1 
    ST:upnp:rootdevice
    USN:uuid:81d520cd-90cd-422d-9cbb-a0287e467e79::urn:schemas-upnp-org:device:Basic:1

From this message you can use the `Location` header to get information about the guhd server. The server will present it self as Basic 1.0 device. At this point you already know the IP address of the server in the network. The server information will be available as xml document and can be accessed by performing a HTTP `GET` request to the `Location` header:

    GET http://10.10.10.50:3333/server.xml

The response will look like this:

    <?xml version="1.0" encoding="UTF-8"?>
    <root xmlns="urn:schemas-upnp-org:device-1-0">
        <specVersion>
            <major>1</major>
            <minor>1</minor>
        </specVersion>
        <URLBase>http://10.10.10.50:3333</URLBase>
        <websocketURL>ws://10.10.10.50:4444</websocketURL>
        <presentationURL>/</presentationURL>
        <device>
            <deviceType>urn:schemas-upnp-org:device:Basic:1</deviceType>
            <friendlyName>guhd</friendlyName>
            <manufacturer>guh</manufacturer>
            <manufacturerURL>http://guh.guru</manufacturerURL>
            <modelDescription>Home automation server</modelDescription>
            <modelName>guhd</modelName>
            <modelNumber>0.6.0</modelNumber>
            <modelURL>http://guh.io</modelURL>
            <UDN>uuid:81d520cd-90cd-422d-9cbb-a0287e467e79</UDN>
            <iconList>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>8</width>
                    <height>8</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-8x8.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>16</width>
                    <height>16</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-16x16.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>22</width>
                    <height>22</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-22x22.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>32</width>
                    <height>32</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-32x32.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>48</width>
                    <height>48</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-48x48.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>64</width>
                    <height>64</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-64x64.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>120</width>
                    <height>120</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-120x120.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>128</width>
                    <height>128</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-128x128.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>256</width>
                    <height>256</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-256x256.png</url>
                </icon>
                <icon>
                    <mimetype>image/png</mimetype>
                    <width>512</width>
                    <height>512</height>
                    <depth>8</depth>
                    <url>/icons/guh-logo-512x512.png</url>
                </icon>
            </iconList>
        </device>
    </root>
   












