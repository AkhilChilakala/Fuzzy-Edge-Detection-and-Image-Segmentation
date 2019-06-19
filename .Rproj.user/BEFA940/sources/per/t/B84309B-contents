library(shiny)
library(imager)
library(FuzzyR)
library(EBImage)
res <- NULL
gr <- NULL
final <- NULL
fis <- newfis("EdgeDetector")
fis <- addvar(fis,"input","gradient-x",c(-1,1))
fis <- addvar(fis,"input","gradient-y",c(-1,1))
fis <- addmf(fis,"input",1,"gauss-x","gaussmf",c(0.1,0))
fis <- addmf(fis,"input",2,"gauss-y","gaussmf",c(0.1,0))
fis <- addvar(fis,"output","res",c(0,1))
fis <- addmf(fis,"output",1,"white","trimf",c(0.3,1,1))
fis <- addmf(fis,"output",1,"black","trimf",c(0,0,0.7))
fis <- addrule(fis,c(1,1,1,1,1))
fis <- addrule(fis,c(-1,-1,2,1,2))