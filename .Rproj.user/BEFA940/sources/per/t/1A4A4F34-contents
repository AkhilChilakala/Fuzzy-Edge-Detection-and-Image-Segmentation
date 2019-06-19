library(shiny)
library(imager)
library(FuzzyR)
library(EBImage)

server <- function(input,output){
  source('source.R', local=TRUE)
  observeEvent(input$upload,{
    irgb <- load.image(input$image$datapath)
    igrey <- grayscale(irgb)
    gr <<- imgradient(igrey)
    color <- readImage(input$image$datapath)
    output$plotimage <- renderPlot({
      layout(t(1:2))
      plot(color)
      plot(Image(igrey))
    })
  })
  toListen1 <- reactive({
    list(input$mean1,input$sd1)
  })
  toListen2 <- reactive({
    list(input$mean2,input$sd2)
  })
  observeEvent(toListen1(),{
    fis$input[[1]]$mf[[1]]$params <<- c(as.numeric(input$sd1),as.numeric(input$mean1))
    output$plotmf1 <- renderPlot(plotmf(fis,"input",1))
  })
  observeEvent(toListen2(),{
    fis$input[[2]]$mf[[1]]$params <<- c(as.numeric(input$sd2),as.numeric(input$mean2))
    output$plotmf2 <- renderPlot(plotmf(fis,"input",2))
  })
  toListen11 <- reactive({
    list(input$a1,input$b1,input$c1,input$a2,input$b2,input$c2)
  })
  observeEvent(toListen11(),{
    fis$output[[1]]$mf[[1]]$params <<- c(as.numeric(input$a1),as.numeric(input$b1),as.numeric(input$c1))
    fis$output[[1]]$mf[[2]]$params <<- c(as.numeric(input$a2),as.numeric(input$b2),as.numeric(input$c2))
    output$plotwb <- renderPlot(plotmf(fis,"output",1))
  })
  observeEvent(input$detect,{
    evalfunc <- function(a,b)
    {
      return (evalfis(c(a,b),fis))
    }
    res <<- mapply(evalfunc,gr$x,gr$y)
    res <<- Image(res,dim(gr$x))
    output$plote <- renderPlot(plot(res))
    output$slider <- renderUI({
      sliderInput("slide","Choose Threshold",0,1,0.73,0.01)
    })
  })
  observeEvent(input$slide,{
    final <<- res<input$slide
    output$plote <- renderPlot(plot(final))
  })
  observeEvent(input$segment,{
    label <- bwlabel(fillHull(final))
    output$plotf <- renderPlot(plot(Image(colorLabels(label))))
  })
}