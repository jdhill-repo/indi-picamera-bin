# indi-picamera-bin
INDI PiCamera driver binaries

The indi-picamera driver is an experimental INDI driver for the Raspberry Pi Camera. The current version only supports the V2 camera. The indi-picamera driver makes use of raspiraw, an example app that receives data directly from CSI sensors on the Raspberry Pi. It supports full sensor (raw bayered ), subframed, and binned images. The Bayer pattern of "BGGR" is written to the FITS header if a fullframe, unbinned image is captured. The driver uses internal automatic software sum stacking of roughly 1 second integrations to achieve very long exposures.

The driver does not currently support the following:

	Raspberry Pi V1 Camera

	Subsecond exposures

	Live video

	ST-4 guiding (Pulse guiding is supported)

	Median stacking


To do:

Add INDI config tab -

	User Gain Setting - The gain is currently set near maximum.
	
	Bayer Enable / Disable (Needed for modified cameras)

	User Config Sum / Median Stacking

---------------------------------------------------------------------------------------------------------

# Requirements:

raspiraw - Download and install pre-compiled binaries from https://github.com/jdhill-repo/raspiraw-bin or build from source https://github.com/6by9/raspiraw.

wiringPi - http://wiringpi.com/download-and-install/ - It is highly recommended that you update wiringpi, even if it is already installed.

---------------------------------------------------------------------------------------------------------

# To download and install

# On Raspian

	cd

	git clone https://github.com/jdhill-repo/indi-picamera-bin.git

	cd indi-picamera-bin/Raspbian

	sudo ./setup


# On Mate

	cd

	git clone https://github.com/jdhill-repo/indi-picamera-bin.git

	cd indi-picamera-bin/Mate

	sudo ./setup

-------------------------------------------------------

# Running indi-picamera:

The driver name is 'indi_picamera_ccd'.

To run, add it to the indiserver command line with your other drivers. For example: indiserver -v indi_canon_ccd indi_celestron_gps indi_picamera_ccd

For setting it up with to use with Ekos, select it from list of drivers, or alternatively, 'indi_picamera_ccd' can be typed directly into the driver field box if it does not appear on the drop down list. 

On the INDI configuration tab, set Polling to 250(ms). This seems to work well, especially for guiding.

For guiding, I have tested using the internal guider with Exposures of 1 or 2 seconds, Binning 4x4, Rapid Guide enabled*, with Auto Loop and Send Image checked under the Rapid Guide tab and adjusting the settings from those. These settings have given me sub arc-second guiding. Of course, the driver is installed on the Raspberry Pi that the camera is connected to.

*When not guiding, disable Rapid Guide.

