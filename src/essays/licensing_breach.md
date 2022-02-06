So recently, [Washington State's department of licensing was breached](https://patch.com/washington/seattle/wa-investigates-data-breach-department-licensing), including potentially social security numbers.

This reminds me of a time when the Illinois Attorney Registration and Disciplinary Comission emailed me my social security number in the clear, as my temporary password. I was, um, displeased.

Sometimes I hear that developers handle sensitive data, and so maybe we should have professional standards bodies regulate developers more closely. I think it is a not-so-veiled attempt at keeping bootcampers out of the profession. Even when the disclaim that intention, I think they are lying: perhaps softly lying to themselves. But also, what do the regulators know about data security?

The funny thing is, one of the first things you learn about databases in bootcamp is how important it is to store sensitive data securely, for example by hashing or encrypting sensitive data. Always hash passwords. Why aren't the social security numbers in the Deparment of Licensing database hashed? To be charitable, one can assume that the database was created a long time ago, when the threat landscape was less severe, and this kind of security thinking was not required. But I will bet you this: it wasn't some coding boot camp graduate who made it that way.
