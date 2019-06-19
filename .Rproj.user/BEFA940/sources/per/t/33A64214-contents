library(shiny)

fluidPage( titlePanel("Edge Detection and Image Segmentation"),
  splitLayout(cellWidths = c("70%", "30%"),
    tabsetPanel(id="Tabs",selected = "Choose Image",
              tabPanel("Choose Image",
                       tags$style(type="text/css", "#plotimage { height: 30px; width: 100%; text-align:center; font-size: 20px;}"),
                        plotOutput("plotimage")
              ),
              tabPanel("Choose MF for input 1",
                       tags$style(type="text/css", "#plotmf1 { height: 30px; width: 100%; text-align:center; font-size: 20px;}"),
                       plotOutput("plotmf1")
              ),
              tabPanel("Choose MF for input 2",
                       tags$style(type="text/css", "#plotmf2 { height: 30px; width: 100%; text-align:center; font-size: 20px;}"),
                       plotOutput("plotmf2")
              ),
              tabPanel("Choose what means White and Black",
                       tags$style(type="text/css", "#plotmf2 { height: 30px; width: 100%; text-align:center; font-size: 20px;}"),
                       plotOutput("plotwb")
                       ),
              tabPanel("Fuzzy Edge Detection",
                       tags$style(type="text/css", "#plotmf2 { height: 30px; width: 100%; text-align:center; font-size: 20px;}"),
                       plotOutput("plote")
                       ),
              tabPanel("Object Segmentation",
                       tags$style(type="text/css", "#plotmf2 { height: 30px; width: 100%; text-align:center; font-size: 20px;}"),
                       plotOutput("plotf")
                       )
    ),
    wellPanel(
      conditionalPanel(
        condition = "input.Tabs == 'Choose Image'",
        tags$hr(),
        fileInput("image", "Choose Image File", accept = c('image/png', 'image/jpeg')),
        actionButton("upload","Upload  Image File")
      ),
      conditionalPanel(
        condition = "input.Tabs == 'Choose MF for input 1'",
        sliderInput("sd1","Standard Deviation",0,1,0.1),
        sliderInput("mean1","Mean",0,1,0)
      ),
      conditionalPanel(
        condition = "input.Tabs == 'Choose MF for input 2'",
        sliderInput("sd2","Standard Deviation",0,1,0.1),
        sliderInput("mean2","Mean",0,1,0)
      ),
      conditionalPanel(
        condition = "input.Tabs == 'Choose what means White and Black'",
        tags$h4("For White"),
        sliderInput("a1","a value",0,1,0.3),
        sliderInput("b1","b value ",0,1,1),
        sliderInput("c1","c value",0,1,1),
        tags$hr(),
        tags$h4("For Black"),
        sliderInput("a2","a value",0,1,0),
        sliderInput("b2","b value",0,1,0),
        sliderInput("c2","c value",0,1,0.7)
      ),
      conditionalPanel(
        condition = "input.Tabs == 'Fuzzy Edge Detection'",
        actionButton("detect","Detect Edge"),
        uiOutput("slider")
      ),
      conditionalPanel(
        condition = "input.Tabs == 'Object Segmentation'",
        actionButton("segment","Segment Image")
      )
    )
  )
  
)
