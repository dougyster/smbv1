### Signing Negotiation Background
In an SMBv1 connection, there is a negotiation phase. This phase
includes negotiating whether or not messages need to be signed. The
client and server are each able to say whether they want to 
require signing; if both want to enforce signing, then it will be
enforced. If AT LEAST one of either the client or the server is
opposed to signing or incapable of supporting it, then messages will
not be signed.

Because of this, it is very easy for an attacker to make a connection
to a server and force the messages to be unsigned. As long as the attacker's
side of the connection refuses to enforce signing, it will not be required.
For this reason, we wanted to build our Tamarin model to demonsrate 
what happens when signing is not enabled; we can assume it is trivial or
close to trivial for the attacker to force this situation.

### Current Progress
We have created our skeleton Tamarin code and begun to model the program.
Since the first step in the SMBv1 connection is the TCP handshake, we started
by modeling that. We have a file, "tcp.spthy" that includes the TCP handshake
and its associated lemmas. By defult, Tamarin uses the Dolev-Yao adversary 
(page 16 of the manual), so we are planning to assume Dolev-Yao throughout the 
project, rather than define our own adversary.

We also created an initial model for signing messages and revealing the signed
messages. We have not yet written the lemmas to enforce and test the model, 
so the next step will be to do that and see whether Tamarin can prove that SMBv1
is indeed vulnerable to MitM attacks when it is possible to leave messages
unsigned.
