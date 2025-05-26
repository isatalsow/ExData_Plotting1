Peer Graded Assignment: Exploratory Data Analysis Course Project (week 1)
Load the data set
file_name <- "household_power_consumption.txt"

mainDir = getwd()
rawDir = "data"
dir.create(file.path(mainDir, rawDir))
setwd(file.path(mainDir, rawDir))
destfile <- file.path(getwd(), "household_power_consumption.zip")
if(!file.exists(destfile)){
        url <- "https://archive.ics.uci.edu/ml/machine-learning-databases/00235/household_power_consumption.zip"
        res <- tryCatch(download.file(url, destfile),
                        error=function(e) 1)
}
unzip("household_power_consumption.zip", exdir = "./")
setwd(file.path(mainDir))
dataDir <- file.path(mainDir,rawDir)

 ls -lh household_power_consumption.txt 
-rw-rw-r-- 1 patechoc patechoc 127M Oct 12  2012 household_power_consumption.txt

 wc -l household_power_consumption.txt
2075260 household_power_consumption.txt

 head household_power_consumption.txt 
Date;Time;Global_active_power;Global_reactive_power;Voltage;Global_intensity;Sub_metering_1;Sub_metering_2;Sub_metering_3
16/12/2006;17:24:00;4.216;0.418;234.840;18.400;0.000;1.000;17.000
16/12/2006;17:25:00;5.360;0.436;233.630;23.000;0.000;1.000;16.000
16/12/2006;17:26:00;5.374;0.498;233.290;23.000;0.000;2.000;17.000
16/12/2006;17:27:00;5.388;0.502;233.740;23.000;0.000;1.000;17.000
16/12/2006;17:28:00;3.666;0.528;235.680;15.800;0.000;1.000;17.000
16/12/2006;17:29:00;3.520;0.522;235.020;15.000;0.000;2.000;17.000
16/12/2006;17:30:00;3.702;0.520;235.090;15.800;0.000;1.000;17.000
16/12/2006;17:31:00;3.700;0.520;235.220;15.800;0.000;1.000;17.000
16/12/2006;17:32:00;3.668;0.510;233.990;15.800;0.000;1.000;17.000

m <- matrix(1,nrow=2075259,ncol=9)
m <- as.data.frame(m)
m[,1] <- sapply(m[,1],as.character.Date)
m[,2:9] <- sapply(m[,1],as.factor)
object.size(m)
print(object.size(m),units="Mb")

fulldata <- read.table("<path-your-data>/household_power_consumption.txt", sep=";")
data     <- fulldata[fulldata$Date >= "01/02/2007" & fulldata$Date <= "02/02/2007", ]


 head -n1 household_power_consumption.txt  > subset_household_power_consumption.txt 

 head subset_household_power_consumption.txt 
Date;Time;Global_active_power;Global_reactive_power;Voltage;Global_intensity;Sub_metering_1;Sub_metering_2;Sub_metering_3

egrep -i "(^1/2/2007)|(^2/2/2007)" household_power_consumption.txt  >> subset_household_power_consumption.txt

 head subset_household_power_consumption.txt 
Date;Time;Global_active_power;Global_reactive_power;Voltage;Global_intensity;Sub_metering_1;Sub_metering_2;Sub_metering_3
1/2/2007;00:00:00;0.326;0.128;243.150;1.400;0.000;0.000;0.000
1/2/2007;00:01:00;0.326;0.130;243.320;1.400;0.000;0.000;0.000
1/2/2007;00:02:00;0.324;0.132;243.510;1.400;0.000;0.000;0.000
1/2/2007;00:03:00;0.324;0.134;243.900;1.400;0.000;0.000;0.000
1/2/2007;00:04:00;0.322;0.130;243.160;1.400;0.000;0.000;0.000
1/2/2007;00:05:00;0.320;0.126;242.290;1.400;0.000;0.000;0.000
1/2/2007;00:06:00;0.320;0.126;242.460;1.400;0.000;0.000;0.000
1/2/2007;00:07:00;0.320;0.126;242.630;1.400;0.000;0.000;0.000
1/2/2007;00:08:00;0.320;0.128;242.700;1.400;0.000;0.000;0.000

patechoc@Jarvis:data$ tail subset_household_power_consumption.txt 
2/2/2007;23:50:00;3.624;0.104;241.110;15.000;0.000;0.000;18.000
2/2/2007;23:51:00;3.628;0.104;241.260;15.000;0.000;0.000;18.000
2/2/2007;23:52:00;3.626;0.104;241.070;15.000;0.000;0.000;18.000
2/2/2007;23:53:00;3.700;0.208;240.720;15.400;0.000;0.000;18.000
2/2/2007;23:54:00;3.696;0.226;240.710;15.200;0.000;1.000;17.000
2/2/2007;23:55:00;3.696;0.226;240.900;15.200;0.000;1.000;18.000
2/2/2007;23:56:00;3.698;0.226;241.020;15.200;0.000;2.000;18.000
2/2/2007;23:57:00;3.684;0.224;240.480;15.200;0.000;1.000;18.000
2/2/2007;23:58:00;3.658;0.220;239.610;15.200;0.000;1.000;17.000
2/2/2007;23:59:00;3.680;0.224;240.370;15.200;0.000;2.000;18.000
No missing values

grep "?" subset_household_power_consumption.txt 


pathCode = "/home/patechoc/Documents/COURSE/MOOCs/COURSERA_Datascienc-with-R/course04_Exploratory_Analysis/CODE/Exploratory-Data-AnalysisExData_week01_PlottingAssignmentProject/"
> pathData = paste0(pathCode, "/../data/")
> setwd(pathData)
> data <- read.table(paste0(pathData, "subset_household_power_consumption.txt", collapse = NULL), sep=";")
> class(data)
[1] "data.frame"
> dim(data)
[1] 2881    9
> head(data)
        V1       V2                  V3                    V4      V5               V6             V7             V8             V9
1     Date     Time Global_active_power Global_reactive_power Voltage Global_intensity Sub_metering_1 Sub_metering_2 Sub_metering_3
2 1/2/2007 00:00:00               0.326                 0.128 243.150            1.400          0.000          0.000          0.000
3 1/2/2007 00:01:00               0.326                 0.130 243.320            1.400          0.000          0.000          0.000
4 1/2/2007 00:02:00               0.324                 0.132 243.510            1.400          0.000          0.000          0.000
5 1/2/2007 00:03:00               0.324                 0.134 243.900            1.400          0.000          0.000          0.000
6 1/2/2007 00:04:00               0.322                 0.130 243.160            1.400          0.000          0.000          0.000

Convert Date & Date+Time 

df$Date <- as.Date(df$Date, format="%d/%m/%Y")
df <- transform(df, timestamp=as.POSIXct(paste(Date, Time)), "%d/%m/%Y %H:%M:%S")


PLOT 1
par(mfrow = c(1,1))
hist(df$Global_active_power, col = "red", main = paste("Global Active Power"),
     xlab = "Global Active Power (kilowatts)")
dev.copy(png, file="plot1.png", width=480, height=480)


PLOT 2
par(mfrow = c(1,1))
plot(df$timestamp,df$Global_active_power, type="l",
     xlab="",
     ylab="Global Active Power (kilowatts)")
dev.copy(png, file="plot2.png", width=480, height=480)
dev.off()

PLOT 3
png(width=480, height=480, file = "plot3.png")
par(mfrow = c(1,1), mar = c(4,4,2,1), oma = c(0,0,2,0))
with(df, {
        plot(Sub_metering_1 ~ timestamp, type = "l", 
             ylab = "Energy sub metering", xlab = "")
        lines(Sub_metering_2 ~ timestamp, col = 'Red')
        lines(Sub_metering_3 ~ timestamp, col = 'Blue')
})
legend("topright", col = c("black", "red", "blue"), lty = 1, lwd = 2, 
       legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"))
dev.off()

PLOT 4
png(width=480, height=480, file = "plot4.png")
par(mfrow = c(2,2), mar = c(4,4,2,1), oma = c(0,0,2,0))
with(df, {
        plot(Global_active_power ~ timestamp, type = "l", 
             ylab = "Global Active Power", xlab = "")
        plot(Voltage ~ timestamp, type = "l", ylab = "Voltage", xlab = "datetime")
        plot(Sub_metering_1 ~ timestamp, type = "l", ylab = "Energy sub metering",
             xlab = "")
        lines(Sub_metering_2 ~ timestamp, col = 'Red')
        lines(Sub_metering_3 ~ timestamp, col = 'Blue')
        legend("topright", col = c("black", "red", "blue"), lty = 1, lwd = 2, 
               bty = "n",
               legend = c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"))
        plot(Global_reactive_power ~ timestamp, type = "l", 
             ylab = "Global_reactive_power", xlab = "datetime")
})



