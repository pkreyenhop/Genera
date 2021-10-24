# Install genera on Ubuntu

```
#
sudo apt-get -y install curl
mkdir $HOME/genera
cd $HOME/genera
curl -L -O https://archives.loomcom.com/genera/genera
chmod a+x genera
#
curl -L -O https://archives.loomcom.com/genera/worlds/Genera-8-5-xlib-patched.vlod
curl -L -O https://archives.loomcom.com/genera/worlds/VLM_debugger
curl -L -O https://archives.loomcom.com/genera/worlds/dot.VLM
cp dot.VLM .VLM
#
cd /var/lib
sudo curl -L -O https://archives.loomcom.com/genera/var_lib_symbolics.tar.gz
sudo tar xvf var_lib_symbolics.tar.gz
sudo chown -R 1000:1000 symbolics
#
cd ~/genera
sed -i '/worldSearchPath/c\genera.worldSearchPath: /home/pkreyenhop/genera' .VLM
cp .VLM .VLM.bup
#
sudo sed -i '/127.0.1.1/a\192.168.2.1    genera-vlm' /etc/hosts
sudo sed -i '/192.168.2.1/a\192.168.2.2    genera' /etc/hosts
#
sudo apt-get -y install inetutils-inetd
sudo sed -i '$a\time      stream  tcp  nowait root internal' /etc/inetd.conf
sudo sed -i '$a\time      dgram   udp  wait   root internal' /etc/inetd.conf
sudo sed -i '$a\daytime   stream  tcp  nowait root internal' /etc/inetd.conf
sudo sed -i '$a\daytime   dgram   udp  wait   root internal' /etc/inetd.conf
sudo systemctl restart inetutils-inetd.service
#
sudo apt-get -y install nfs-common nfs-kernel-server
sudo sed -i '$a\/       genera(rw,sync,no_subtree_check,all_squash,anonuid=1000,anongid=1000)' /etc/exports
sudo systemctl restart nfs-kernel-server
#
sudo sed -i '/RPCNFSDCOUNT=8/c\RPCNFSDCOUNT="--nfs-version 2 8"' /etc/default/nfs-kernel-server
sudo sed -i '/RPCMOUNTDOPTS="--manage-gids"/c\RPCMOUNTDOPTS="--nfs-version 2 --manage-gids"' /etc/default/nfs-kernel-server
sudo systemctl restart nfs-kernel-server
#
sudo ip tuntap add dev tap0 mode tap
sudo ip addr add 192.168.2.1/24 dev tap0
sudo ip link set dev tap0 up
```
# Fn Keys on apple Keyboard 
```
echo 2 | sudo tee /sys/module/hid_apple/parameters/fnmode
```

# Key Mapping
```
m option
s command

<rubout> del or fn+backspace
<select> f1
<resume> f5
<abort>  f6
<clear> f10
<help>  f12
<scroll> f9



```

# Select Keys
```
<select>+<help> Select Key Help

<select>+e Editor
<select>+l Lisp
<select>+d Document examiner


```

# Keyboard History
```
c-m-Y - last entry
m-Y   - next back
```


# Set Lisp Syntax in Editor
`m-X set lisp syntax `

# Editor Commands
```
m-X compile buffer
m-X set package
c-shift-C compile deinition

m-. go to definitiomn
m-<left mouse click> go to definition

c-shift-A show input variables

c-m-e go to end of outer s-expression
c-; comment at end of line
c-s-U undo
c-X c-; comment out s-expression
c-m-\ format code
c-% find and replace all

c-m-K kill s-expression forward (cut)
c-Y yanks s-expresion (paste)

```

# Show Documentation for Lisp Functions
```
Show Doc <lisp function>
Example: show doc reverse 
```

















