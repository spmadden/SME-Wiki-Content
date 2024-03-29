# Kernel Flags to enable in 6.1.0:

``` bash
# I know what I'm doing - unlock the good stuff.
CONFIG_EXPERT=y

# Yes, I acknowledge it's on me to NOT break the law.
CONFIG_CFG80211_CERTIFICATION_ONUS=y 
        bool "cfg80211 certification onus"
        depends on EXPERT
        default n
        help
          You should disable this option unless you are both capable
          and willing to ensure your system will remain regulatory
          compliant with the features available under this option.
          Some options may still be under heavy development and
          for whatever reason regulatory compliance has not or
          cannot yet be verified. Regulatory verification may at
          times only be possible until you have the final system
          in place.

          This option should only be enabled by system integrators
          or distributions that have done work necessary to ensure
          regulatory certification on the system with the enabled
          features. Alternatively you can enable this option if
          you are a wireless researcher and are working in a controlled
          and approved environment by your local regulatory agency.


# Allow unsigned regulatory law databases
CONFIG_CFG80211_REQUIRE_SIGNED_REGDB=n
        bool "require regdb signature" if CFG80211_CERTIFICATION_ONUS
        default y
        select SYSTEM_DATA_VERIFICATION
        help
          Require that in addition to the "regulatory.db" file a
          "regulatory.db.p7s" can be loaded with a valid PKCS#7
          signature for the regulatory.db file made by one of the
          keys in the certs/ directory.


# Allow the ability to transmit where laws say you can't
CONFIG_CFG80211_REG_RELAX_NO_IR=y
        bool "cfg80211 support for NO_IR relaxation"
        depends on CFG80211_CERTIFICATION_ONUS
        help
         This option enables support for relaxation of the NO_IR flag for
         situations that certain regulatory bodies have provided clarifications
         on how relaxation can occur. This feature has an inherent dependency on
         userspace features which must have been properly tested and as such is
         not enabled by default.

         A relaxation feature example is allowing the operation of a P2P group
         owner (GO) on channels marked with NO_IR if there is an additional BSS
         interface which associated to an AP which userspace assumes or confirms
         to be an authorized master, i.e., with radar detection support and DFS
         capabilities. However, note that in order to not create daisy chain
         scenarios, this relaxation is not allowed in cases where the BSS client
         is associated to P2P GO and in addition the P2P GO instantiated on
         a channel due to this relaxation should not allow connection from
         non P2P clients.

         The regulatory core will apply these relaxations only for drivers that
         support this feature by declaring the appropriate channel flags and
         capabilities in their registration flow.


# Allow the user to override the firmware regulatory settings in Atheros chipsets
CONFIG_ATH_REG_DYNAMIC_USER_REG_HINTS=y 
        bool "Atheros dynamic user regulatory hints"
        depends on CFG80211_CERTIFICATION_ONUS
        default n
        help
          Say N. This should only be enabled in countries where
          this feature is explicitly allowed and only on cards that
          specifically have been tested for this.


# Signify to the atheros driver that we're doing "certification testing"
CONFIG_ATH_REG_DYNAMIC_USER_CERT_TESTING=y
        bool "Atheros dynamic user regulatory testing"
        depends on ATH_REG_DYNAMIC_USER_REG_HINTS && CFG80211_CERTIFICATION_ONUS
        default n
        help
          Say N. This should only be enabled on systems
          undergoing certification testing.

# Signify to the driver that we're in an approved transmit area.
CONFIG_ATH10K_DFS_CERTIFIED=y
        bool "Atheros DFS support for certified platforms"
        depends on ATH10K && CFG80211_CERTIFICATION_ONUS
        default n
        help
            This option enables DFS support for initiating radiation on
            ath10k.
```

# hostapd.conf

``` bash
ctrl_interface=/var/run/hostapd
ctrl_interface_group=wheel

# Some usable default settings...
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0

# WPA version 3
wpa=3
# WPA pre-shared key
wpa_key_mgmt=WPA-PSK
# Use TKIP
wpa_pairwise=TKIP
# and CCMP
rsn_pairwise=CCMP

# DO NOT FORGET TO SET A WPA PASSPHRASE!!
wpa_passphrase=<passphrase>
ssid=<ssid>

# Most modern wireless drivers in the kernel need driver=nl80211
driver=nl80211

# Customize these for your local configuration...
interface=wlp5s0
bridge=bridge0

# 5 GHz Band:
hw_mode=a
# channel 0 means 'scan for open channel'
channel=0


country_code=US
# Indoor only
#country3=0x49
# Outdoor only
#country3=0x4f
# All everything
country3=0x20
#local_pwr_constraint=30

# enable WMM (required for full N/AC functionality
wmm_enabled=1

# advertize country code
ieee80211d=1
# DFS and radar detection
ieee80211h=1
# enable N [ht]
ieee80211n=1
# enable AC [vht]
ieee80211ac=1
# enable AX [he]
#ieee80211ax=1
# allow short preamble
preamble=1

#vht_oper_centr_freq_seg0_idx=42
#vht_oper_centr_freq_seg1_idx=159

# 5 scan cycles to find an open channel
acs_num_scans=5

# Choose the channels you want to scan.
#chanlist=1-11 32-68 100-177
chanlist=1-11 50-68 100-177

# use 'iw list' to see what your card supports
# HT is Wireless "N" parameters - customize to your card.  
ht_capab=[LDPC][HT40+][TX-STBC][RX-STBC1][MAX-AMSDU-7935][DSSS_CCK-40]
# VHT is Wireless "AC" parameters - customize to your card.
vht_capab=[MAX-MPDU-11454][RXLDPC][SHORT-GI-80][TX-STBC-2BY1][RX-ANTENNA-PATTERN][TX-ANTENNA-PATTERN]
# set channel width - 0 = 20/40, 1 = 80, 2 = 160, 3 = 80+80
vht_oper_chwidth=1

# HE is Wireless "AX" parameters - customize to your card.
# he_capab=[]

```
