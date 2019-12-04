# Orchestration

## Rancher

Easy to use, just drag and drop things.

## Benefits of using Docker

	- escape the app dependency matrix
	- Solve the environment issue. it works on my machine.
## Network

- Bridge
- Host

## Tips

	- difference between `cmd` and `entrypoint`
	- difference between `copy` and `add`

        Basically they are similar, copy files and folder to destination. While ADD has some features (like local-only tar extraction and remote URL support) that are not immediately obvious. Consequently, the best use for ADD is local tar file auto-extraction into the image, as in ADD rootfs.tar.xz /.
- CMD
	- has three forms
		- CMD ["executable","param1","param2"]
			- exec form, preferred
		- CMD ["param1","param2"]
			- as default parameters to ENTRYPOINT
		- CMD command param1 param2
			- shell form
	- The main purpose of a CMD is to provide defaults for an executing container. These defaults can include an executable, or they can omit the executable, in which case you must specify an ENTRYPOINT instruction as well.
	- If CMD is used to provide default arguments for the ENTRYPOINT instruction, both the CMD and ENTRYPOINT instructions should be specified with the JSON array format.
	- docker run could override the default specified in CMD.
- ENTRYPOINT
	- docker run arguments will as the entrypoint’s parameters. not CMD’s override
	- has two forms
		- ENTRYPOINT ["executable", "param1", "param2"]
			- exec form, preferred
		- ENTRYPOINT command param1 param2
			- shell form
	- entrypoint setting can be override by docker run —entrypoint
- Security
	- https://docs.docker.com/engine/security/security/
	- use non root user
	- docker daemon attack surface
	- kernel security features
