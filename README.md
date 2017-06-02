# REKSI
<a href="http://www.awkene.com">SOURCE</a>
<h2>Reksi is a awsome little script for spoofing your mac address using random macs and default!</h2>
<pre>
import os, sys, time
import random
import fcntl, socket, struct
from pyfiglet import Figlet

def getHwAddr(ifname):
    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    info = fcntl.ioctl(s.fileno(), 0x8927,  struct.pack('256s', ifname[:15]))
    return ':'.join(['%02x' % ord(char) for char in info[18:24]])

os.system('clear')
f = Figlet(font='slant')
print f.renderText('REKSI') #/Banner/
print "REKSI Random macs and more spoofing nerdy stuff\n"
macop = raw_input("[start random mac address? Y/n]-[-] ") #/Option for random mac or default/
inter = raw_input("[interface@reksi]-[-] ") #/Input your interface/

time.sleep(0.2)
print "your current mac address:", getHwAddr((inter))

if macop == 'Y':
    mac = [ 0x00, 0x16, 0x3e,
    random.randint(0x00, 0x7f),
    random.randint(0x00, 0xff),
    random.randint(0x00, 0xff) ]
    macd = ':'.join(map(lambda x: "%02x" % x, mac))
    os.system("ip link set dev " + inter + " down")
    os.system("ip link set dev " + inter + " address " + macd + "")
    os.system("ip link set dev " + inter + " up")
else:
    mex = "7c:0b:c6:43:1f:0a" #/Your new mac address/
    os.system("ip link set dev " + inter + " down")
    os.system("ip link set dev " + inter + " address " + mex + "")
    os.system("ip link set dev " + inter + " up")


print "old mac address [CHANGED!]"
time.sleep(0.2)
print "[ !WARNING ] please wait restarting network settings [ WARNING! ]\n"
time.sleep(0.5)
os.system('service network-manager restart')
print "Ok!, your new mac address is:", getHwAddr((inter))

</pre>
