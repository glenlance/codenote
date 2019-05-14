go generate永远不会由go build、go get、go test等自动运行。必须显式运行。
go generate扫描文件中的指令，这些指令是表单的行，