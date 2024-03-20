import tkinter as tk
import telnetlib


WORK_ULTRA_IP = "10.14.128.49" # Change to your IP 
IP_ADDRESS = ""


def telnet_to_device(ip_address):
    try:
        tn = telnetlib.Telnet(ip_address, 8080)
        Astr = tn.read_until(b"Uv7LYYXoe3", 1)
        print("Telnet connection successful!")
        return tn
    except Exception as e:
        print("Telnet connection failed:", e)

def change_location(tn, country_code, locale_code):
    if tn:
        try:
            tn.write(f"country {country_code}\r\n".encode())
            print(f"SENT: country {country_code}")
            Astr = tn.read_until(b">", 10)
            print("RECEIVED:")
            print(Astr.decode())
            print()

            tn.write(f"cscountry {country_code}\r\n".encode())
            print(f"SENT: cscountry {country_code}")
            Astr = tn.read_until(b">", 1)
            print("RECEIVED:")
            print(Astr.decode())
            print()

            tn.write(f"locale {locale_code}\r\n".encode())
            print(f"SENT: locale {locale_code}")
            Astr = tn.read_until(b">", 20)
            print("RECEIVED:")
            print(Astr.decode())
            print()

            if country_code == 'mx':
                tn.write(b"reboot\r\n")
                print("SENT: reboot")
                Astr = tn.read_until(b"Uv7LYYXoe3", 1)
                print("RECEIVED:")
                print(Astr.decode())
                print()

            tn.close()
        except Exception as e:
            print("Error:", e)

def change_to_us():
    ip_address = ip_address_entry.get()
    tn = telnet_to_device(ip_address)
    change_location(tn, 'us', 'en_us')

def change_to_ca():
    ip_address = ip_address_entry.get()
    tn = telnet_to_device(ip_address)
    change_location(tn, 'ca', 'en_ca')

def change_to_mx():
    ip_address = ip_address_entry.get()
    tn = telnet_to_device(ip_address)
    change_location(tn, 'mx', 'es_mx')

root = tk.Tk()
root.title("Baby Commander")

# Label for IP Address
ip_label = tk.Label(root, text="Enter Device IP Address:")
ip_label.grid(row=0, column=0, padx=5, pady=5, sticky="w")

# Entry for IP Address
ip_address_entry = tk.Entry(root, width=20)
ip_address_entry.grid(row=0, column=1, padx=5, pady=5)

# Button to change to US
change_us_button = tk.Button(root, text="Change Location to US 🇺🇸", command=change_to_us)
change_us_button.grid(row=1, column=0, columnspan=2, padx=5, pady=5, sticky="we")

# Button to change to CA
change_ca_button = tk.Button(root, text="Change Location to CA 🇨🇦", command=change_to_ca)
change_ca_button.grid(row=2, column=0, columnspan=2, padx=5, pady=5, sticky="we")

# Button to change to MX
change_mx_button = tk.Button(root, text="Change Location to MX 🇲🇽", command=change_to_mx)
change_mx_button.grid(row=3, column=0, columnspan=2, padx=5, pady=5, sticky="we")

root.mainloop()
