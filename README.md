# My_leaflet_proof
library(raster)

library (leafpop)

library(sf)

library(leaflet)

library(lattice)

library(shiny)

TUNISIA <- getData(name="GADM",  country="TUN", level=1)

Site1 = st_as_sf(data.frame(x = 9.18513888888889, y = 36.7239444),
                 coords = c("x", "y"),
                 crs = 4326)
                 
html_legend <- "<img src=' https://raw.githubusercontent.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-blue.png '>Presence "

tag.Ailanthus.Altissima.in.Tunisia<- tags$style(HTML("

  .leaflet-control.Ailanthus-Altissima-in-Tunisia{
  
    transform: translate(-50%,20%);
    
    position: fixed !important;
    
    left: 50%;
    
    text-align: center;
    
    padding-left: 10px; 
    
    padding-right: 10px; 
    
    background: rgba(255,255,255,0.3);
    
    font-weight: bold;
    
    font-size: 20px;
  }
"))


title <- tags$div(
    tag.Ailanthus.Altissima.in.Tunisia, HTML("Ailanthus Altissima in Tunisia")
)

leaflet() %>% 
    addProviderTiles(providers$Esri.WorldImagery) %>%
    addPolygons(data= TUNISIA, fillOpacity = 0, weight = 2.5, color = '#FF1900', dashArray = "0")%>% 
    addControl(title, position = "topleft", className="Ailanthus-Altissima-in-Tunisia")%>%
    addCircleMarkers(radius =5, 
                     stroke = FALSE, 
                     fillOpacity = 0.4,
                     lng=9.18513888888889, lat= 36.7239444)%>%
    addMarkers (data = Site1, group = "Site1", popup = paste(sep = "<br/>",
                                                             "Prospecteur: Zayneb Soilhi")) %>%
    addPopupImages(image, group = "Site1", width = 500, maxWidth = 500) %>%
    addControl(html = html_legend, position = "bottomright")
    
