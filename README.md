# hidden_browser
Hiding a Tor Browser Bundle but making it easy to open--if you know how

The goal of the project is to allow a user to access a Tor Browser Bundle with minimal training and no knowledge of cryptography, or even the password for the encrypted archive, and without requiring any form of elevated credentials.

The intended audience is people who need access to certain kinds of sites but cannot risk going to them using a normal browser.  For instance, a closeted homosexual who wishes to visit support sites but cannot because of filtering or other electronic monitoring, but who gets access to the computer without someone over their shoulder.

At the moment, the thought is to tuck the encrypted archive (encrypted using the SHA1 or SHA256 hash of a keyfile) away in the Alternate Data Stream of an innocuous file.  The archive would be extracted by a specific key sequence (eventually be custom to each implementation) from within an executable that has some obvious purpose but also this hidden purpose.  Entering the key sequence would trigger a script to decrypt and extract the archive contents and run the browser.  The script would continue to run in the background to monitor both the original application and the TBB every few seconds.  If either is terminated, the script would terminate the other and delete the extracted archive (ideally securely), and then exit itself.

Additional visibility protection could be added by using tiny USB drives such as the Sandisk Low Profile Drive.  The user might be able to tuck this away in an inconspicuous USB slot, making it even less likely to be spotted.

This setup would allow cursory inspection of the drive's contents without revealing the presence of the archive.  It does not hide the TBB once launched, but by a simple action to close (Alt-F4, Alt-Q, clicking the X), it does nix the presence of the software quickly.

I realize the issues surrounding something like this.  They include, in no particular order:
- "Password" recovery possible by decompiling the code and looking for the key sequences.
- Finding data in ADS is trivial for anyone who knows how to do it.
- This requires NTFS.
- This breaks any form of auto-update for TBB.
- Some filters are getting better at blocking Tor.
- Straight deletion of the files may be recovered using trivial forensic options.
- Settings that block unsigned software would prevent the original application from running.

There are almost certainly other issues.  Some of the issues present prevent certain "obvious" solutions:
- TrueCrypt/VeraCrypt solutions are out because even in portable mode, they require elevated privileges to run the driver.
- WIM mounting via PowerShell is out because it requires elevated privileges to run.
- Various secure deletion options require elevated privileges to run.

That said, this may give some people options that they otherwise don't have.  Still much to explore on how to mitigate things and make it easy for users.  It should be interesting.
