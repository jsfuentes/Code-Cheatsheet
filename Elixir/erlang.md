# Erlang

Built by telecoms systems(Ericson in 1970s ) and run most of the worlds communications(5 9's more with Erlang)

Erlang is highly scalable and lightweight, like can be its own OS on very lightweight systems(100x smaller/startup time) 

Very reliablity b/c not general purpose, runs threadlike erlang code only(scales linear up to 50 cores)

Each process runs 1000 cycles then gives up, processes can't block or anything. So multicores parallelism, balancing across cores, and adding more processes is trivial and automatic. Can take yourself out of rotation while waiting for messages(IO too). And rebooting when process crash is automatic. Low latecny over throughput. 

### OTP

Supervisor looks over Genserver

Erlang used by Heroku, WhatsApp(2 million connections on a single machine);

