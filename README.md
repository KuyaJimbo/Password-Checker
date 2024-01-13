# Summary
This Python script checks if a given password has been previously exposed in data breaches. It ues the Pwned Passwords API, which allows checking passwords against a database of known compromised passwords.

## The Cool Part
Instead of sending the **entire** user-provided password, the script sends **only the first 5 characters** of its **hashed form** to the *Pwned Passwords API*. This hashed representation **ensures privacy during the check**.

The API responds with a list of hashed passwords and their counts. The script then looks for a match with the remaining characters of the user's hashed password. If found, it suggests that the password has been compromised, and the count is reported. 

***This approach balances password security verification with user privacy.***

## Functions
`requests_api_data(query_char)`
Takes a string query_char, which represents the first 5 characters of a SHA-1 hashed password.
Constructs the API URL with the provided query_char.
Sends a GET request to the Pwned Passwords API.
Returns the response.

`get_password_leaks_count(hashes, hash_to_check)`
Takes the API response (hashes) and the remaining part of the SHA-1 hashed password (hash_to_check).
Parses the API response into a list of tuples (hash, count).
Checks if the given hash_to_check is in the list and returns the corresponding count if found.

`pwned_api_check(password)`
Takes a plain text password as input.
Converts the password to a SHA-1 hash.
Divides the hash into the first 5 characters (first5_char) and the rest (tail).
Calls requests_api_data with first5_char to get a response from the API.
Calls get_password_leaks_count to check if the hash exists in the response and returns the count if found.

`main(args)`
Takes a list of passwords as command-line arguments.
Iterates through each password, calling pwned_api_check.
Prints a message indicating whether the password was found in data breaches and how many times.
Exits the script.

`if name == 'main'`
Ensures that the main function is executed only if the script is run directly, not when imported as a module.

## Requests Library Usage:
This program requires the *Requests* library to be installed. To install *Requests*, run the following command in the terminal:

`pip install requests`
