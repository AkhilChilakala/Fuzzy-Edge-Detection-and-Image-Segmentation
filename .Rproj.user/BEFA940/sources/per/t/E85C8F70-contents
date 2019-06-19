library(imager)
library(FuzzyR)
library(EBImage)

irgb <- load.example("coins")
igrey <- grayscale(irgb)
gr <- imgradient(igrey)

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

evalfunc <- function(a,b)
{
  return (evalfis(c(a,b),fis))
}

res <- mapply(evalfunc,gr$x,gr$y)
res <- Image(res,dim(gr$x))

final <- res<0.73
label <- bwlabel(fillHull(final))

layout(t(1:3))
plot(Image(irgb))
plot(Image(final))
plot(Image(colorLabels(label)))

writeImage(Image(coins),"coins.jpg")
writeImage(Image(colorLabels(label)),"Segmented Output.jpg")
