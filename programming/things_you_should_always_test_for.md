# Inputs

     - Minimum and maximum input values are always good to test. For instance, if a password field allows 6 to 128 characters, what actually happens when you submit a six-character password? What about a 128-character password?
    - Too-high and too-low values. What happens with a 5-character or 129-character password? Alternately, how does the system respond to inputs equal to the the minimum and maximum integer values allowed by the implementation language or platform?
    - Invalid values such as null and NaN. Strings instead of integers, arrays instead of strings.
    - Inputs that might break the underlying code. For a Web app examples would include SQL injection and cross-site scripting attacks.
    - Empty inputs such as a blank user name field or a transaction record in which none of the fields contain any information. For unit tests, submitting zero or an empty string instead of a valid parameter can sometimes yield interesting results.
    - Inputs that are too big, perhaps even too big to conveniently fit into available memory…
    - Too many inputs or not enough inputs. For a unit test this is simply a matter of creating an incorrect function signature. For a Web app it might involve submitting too many POST parameters or selectively deleting parts of a URL’s query string.

# Math

1.  Decimal math is hard. Verify that integers are treated correctly in a floating-point context, and vice versa.
2.  Repeating decimals. Does the system treat 0.666 differently from 0.665?
3.  Rounding. If you put 3 \* 1.005 into the system, do you get 3.015 back out? (This is not the default behavior in JavaScript, for instance.)
4.  Type coercion. Is an input of 23 treated differently than an input of "23"? That is: is a numeric input treated differently than a string containing a numeric value?
5.  Units of measurement. If you specify that the thrusters should fire with a force of 267 Newtons, does the guidance system actually interpret that value as Newtons? Or is it interpreted as 267 foot-pounds? (Hat tip to Sebastian Delmont for pointing out that units of measurement are worth testing.)
6.  Units of currency. There’s going to be a problem if an input of £23.00 is stored in the database as \$23.00.

# Text

1.  User names are perhaps the single most interesting class of text that can be submitted as input to a computer program. At a minimum, the system shouldn’t break when names contain apostrophes, hyphens or spaces.
2.  Passwords are also interesting. Does the maximum password length allow for enough entropy? Are plain-English passphrases disallowed because they don’t contain numbers? Are passwords stored as salted hashes?
3.  Are Unicode inputs treated differently than ASCII?
4.  On the Web, are HTML-encoded entities properly converted to characters and vice versa? What about URL-encoded characters?

# Time

1.  Time zones are a bitch. Try switching the system time from GMT to EST and see what happens.
2.  Test on the first and last day of daylight savings time. The system does allow you to mock out the first and last day of daylight savings time, right?
3.  Like with unit tests, boundary conditions can reveal interestingness. How does the system behave between 23:59 and 00:01? What about during the hour between 00:00 and 00:59?
4.  Be very aware of dates and times that are “special” to your system. For instance, if you have a fake user for testing purposes, how does the system respond when it’s that user’s birthday?

# System resources

1.  What if there’s half as much available memory as the system’s designers expect?
2.  In a distributed system, what happens if half the nodes become unavailable?
3.  In a service-oriented architecture, what happens if one of the services becomes unavailable? What if it’s only partially available?
4.  What happens if the network is slow?
5.  What happens when the database is down?
6.  What happens when the database is empty?
7.  What happens if the cache is disabled? What about the CDN?
8.  What if load on the system spikes to ten times normal?
9.  What if load on the system drops to zero?
10. For long-running operations, what happens if you power cycle the machine before the operation is complete?
