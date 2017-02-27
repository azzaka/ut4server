FROM centos:6
MAINTAINER Garrett McGrath <gmcgrath815+docker at gmail.com>

RUN yum install -y wget unzip; /usr/bin/wget "https://s3.amazonaws.com/unrealtournament/UnrealTournament-Server-XAN-3315666-Linux.zip" -O temp.zip; /usr/bin/unzip temp.zip; rm temp.zip

RUN yum install -y Xvfb xorg-X11-server-Xvfb which

RUN chmod +x /LinuxServer/Engine/Binaries/Linux/*

#this is where you SHOULD be able to mount the confs file and have it 'just work' that's not the case however.
#VOLUME ["/LinuxServer/UnrealTournament/Saved/Config/LinuxServer"]

#stupid hack version of problem fixing
#This hack works around the docker version of the server dumping all it's confs inside
#/LinuxServer/UnrealTournament instead of inside /LinuxServer/UnrealTournament/Saved/Config/LinuxServer because reasons?

VOLUME ["/conf"] 

#if reason for issue is located this should just be symlinked to /LinuxServer above

RUN ln -s /conf/Engine.ini /LinuxServer/UnrealTournament/Engine.ini; \
ln -s /conf/Game.ini /LinuxServer/UnrealTournament/Game.ini; \
ln -s /conf/GameUserSettings.ini /LinuxServer/UnrealTournament/GameUserSettings.ini; \
ln -s /conf/Compat.ini /LinuxServer/UnrealTournament/Compat.ini; \
ln -s /conf/DeviceProfiles.ini /LinuxServer/UnrealTournament/DeviceProfiles.ini; \
ln -s /conf/Input.ini /LinuxServer/UnrealTournament/Input.ini; \
ln -s /conf/Lightmass.ini /LinuxServer/UnrealTournament/Lightmass.ini; \
ln -s /conf/Rules.ini /LinuxServer/UnrealTournament/Rules.ini; \
ln -s /conf/SampleGameMode.ini /LinuxServer/UnrealTournament/SampleGameMode.ini; \
ln -s /conf/Scalability.ini /LinuxServer/UnrealTournament/Scalability.ini

#this saves a bunch of typing when trying to configure the system
RUN ln -s /conf /LinuxServer/UnrealTournament/Saved/Config/LinuxServer 

EXPOSE 7777/udp 13000udp 15000/udp 7787/udp

CMD ["/usr/bin/xvfb-run","/LinuxServer/Engine/Binaries/Linux/UE4Server-Linux-Test","UnrealTournament","DM-DeckTest?Game=DM?MaxPlayers=20?MaxSpectators=15","-log","-port=7777"]
