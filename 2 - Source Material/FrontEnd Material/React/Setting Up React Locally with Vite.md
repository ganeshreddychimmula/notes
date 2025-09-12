
2025-06-24 12:18

Status:

Tags: [[Setup]] [[../../../3 - Tags/React]]


---
# Setting Up React Locally with Vite
[**Link to the video Src**](https://scrimba.com/learn-react-c0e/~04xn)
### Installing node and npm (ONly First time)
- For that you need to already have node and npm.
	- Check `node -v`(18 and above) and  `npm -v`()
- NVM is least painful way to install node and npm
- `nvm install --lts` (long term supported version) gives you the most stable version of node.
### Starting a new project
- `npm create vite@latest` - This is start a process that will help build the project
![[Pasted image 20250624130402.png]]

![[Pasted image 20250624130438.png]]

![[Pasted image 20250624130520.png]]

- `cd first-react` (project folder)
- `npm install`
- `code .`(optional) -> to open VS Code for that folder
- `npm run dev`
- 


## Installation Errors
- Install latest node
- Remove-Item -Recurse -Force node_modules (Powershell Commands)
- del package-lock.json
- npm run dev
	- npm install vite@latest --save-dev


---
## References
[Build a React  App from Scratch through Vite](https://react.dev/learn/build-a-react-app-from-scratch)
[[Vite Guide]]
[[Understanding Cypto Hash Error - React Setup]]