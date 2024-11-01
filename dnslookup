import socket
import sys

def dns_lookup(ips_or_hostnames):
    results = {}
    for item in ips_or_hostnames:
        item = item.strip()  # Remove any surrounding whitespace
        if not item:
            continue  # Skip empty lines
        try:
            # Check if the item is an IP address
            socket.inet_aton(item)  # Will raise an exception if not a valid IP
            # Get hostname from IP
            hostname = socket.gethostbyaddr(item)[0]
            results[item] = hostname
        except socket.error:
            try:
                # Try to get IP from hostname
                ip = socket.gethostbyname(item)
                results[item] = ip
            except socket.error as e:
                results[item] = f"Error: {e}"

    return results

def read_input_file(filename):
    with open(filename, 'r') as file:
        return file.readlines()

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python dns_lookup.py <input_file>")
        sys.exit(1)

    input_file = sys.argv[1]
    
    try:
        inputs = read_input_file(input_file)
        results = dns_lookup(inputs)
        for item, result in results.items():
            print(f"{item.strip()}: {result}")
    except FileNotFoundError:
        print(f"Error: The file '{input_file}' was not found.")
    except Exception as e:
        print(f"An error occurred: {e}")
