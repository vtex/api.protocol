: <<'END'
Multicultured RAML build script.
END

# Documented API
API="protocol"

# Input RAML directory
INPUTDIR="."

# Output directory
OUTPUTDIR="$INPUTDIR/../raml-output"

if [[ "$1" == "all" ]]; then
	#Verify if output dir exists. If it doesn't exist, it is created
	if [ -d "$OUTPUTDIR" ]; then
		echo -e "\033[0m\033[1mClearing previous build...\033[2m"
		rm -rfv $OUTPUTDIR
	fi

	build "pt-br"
	build "en-us"
	build "es-es"
else
	# DEFAULTCULTURE value
	DEFAULTCULTURE="pt-br"
	CULTURE=$DEFAULTCULTURE

	if [[ "$1" ]]; then
		CULTURE="$1"
	fi

	OUTPUTDIR=$OUTPUTDIR/$CULTURE

	echo $OUTPUTDIR

	mkdir -p $OUTPUTDIR

	echo -e "\033[0m\033[1mCopying $INPUTDIR files...\033[2m"
	cp -v $INPUTDIR/* $OUTPUTDIR

	if [[ -d "$INPUTDIR/documentation" ]]; then
		mkdir $OUTPUTDIR/documentation
		echo -e "\033[0m\033[1mCopying 'documentation' defaults...\033[2m"
		cp $INPUTDIR/documentation/* $OUTPUTDIR/documentation

		echo -e "\033[0m\033[1mCopying default culture documentation...\033[2m"
		cp -Rv $INPUTDIR/documentation/$DEFAULTCULTURE/* $OUTPUTDIR/documentation

		if [[ $DEFAULTCULTURE != $CULTURE ]]; then
			echo -e "\033[0m\033[1mOverriding default culture documentation with '$CULTURE' documentation...\033[2m"
			cp -Rv $INPUTDIR/documentation/$CULTURE/* $OUTPUTDIR/documentation
		fi
	fi

	if [[ -d "$INPUTDIR/examples" ]]; then
		mkdir $OUTPUTDIR/examples
		echo -e "\033[0m\033[1mCopying 'examples' defaults...\033[2m"
		cp $INPUTDIR/examples/* $OUTPUTDIR/examples

		echo -e "\033[0m\033[1mCopying default culture examples...\033[2m"
		cp -Rv $INPUTDIR/examples/$DEFAULTCULTURE/* $OUTPUTDIR/examples

		if [[ $DEFAULTCULTURE != $CULTURE ]]; then
			echo -e "\033[0m\033[1mOverriding default culture examples with '$CULTURE' examples...\033[2m"
			cp -Rv $INPUTDIR/examples/$CULTURE/* $OUTPUTDIR/examples
		fi
	fi

	if [[ -d "$INPUTDIR/resourceTypes" ]]; then
		mkdir $OUTPUTDIR/resourceTypes
		echo -e "\033[0m\033[1mCopying 'resourceTypes' defaults...\033[2m"
		cp $INPUTDIR/resourceTypes/* $OUTPUTDIR/resourceTypes

		echo -e "\033[0m\033[1mCopying default culture resource types...\033[2m"
		cp -Rv $INPUTDIR/resourceTypes/$DEFAULTCULTURE/* $OUTPUTDIR/resourceTypes

		if [[ $DEFAULTCULTURE != $CULTURE ]]; then
			echo -e "\033[0m\033[1mOverriding default culture resource types with '$CULTURE' resourceTypes...\033[2m"
			cp -Rv $INPUTDIR/resourceTypes/$CULTURE/* $OUTPUTDIR/resourceTypes
		fi
	fi

	if [[ -d "$INPUTDIR/schema" ]]; then
		mkdir $OUTPUTDIR/schema
		echo -e "\033[0m\033[1mCopying 'schema' defaults...\033[2m"
		cp $INPUTDIR/schema/* $OUTPUTDIR/schema

		echo -e "\033[0m\033[1mCopying default culture schema...\033[2m"
		cp -Rv $INPUTDIR/schema/$DEFAULTCULTURE/* $OUTPUTDIR/schema

		if [[ $DEFAULTCULTURE != $CULTURE ]]; then
			echo -e "\033[0m\033[1mOverriding default culture schema with '$CULTURE' schema...\033[2m"
			cp -Rv $INPUTDIR/schema/$CULTURE/* $OUTPUTDIR/schema
		fi
	fi

	if [[ -d "$INPUTDIR/traits" ]]; then
		mkdir $OUTPUTDIR/traits
		echo -e "\033[0m\033[1mCopying 'traits' defaults...\033[2m"
		cp $INPUTDIR/traits/* $OUTPUTDIR/traits

		echo -e "\033[0m\033[1mCopying default culture traits...\033[2m"
		cp -Rv $INPUTDIR/traits/$DEFAULTCULTURE/* $OUTPUTDIR/traits

		if [[ $DEFAULTCULTURE != $CULTURE ]]; then
			echo -e "\033[0m\033[1mOverriding default culture traits with '$CULTURE' traits...\033[2m"
			cp -Rv $INPUTDIR/traits/$CULTURE/* $OUTPUTDIR/traits
		fi
	fi

	echo -e "\033[0m\033[1mSetting protocol culture to '$CULTURE'...\033[2m"
	sed "s/{%culture}/$CULTURE/g" $INPUTDIR/$API.raml > $OUTPUTDIR/$API.raml

	echo -e "\033[0m\033[1mBuilding 'index.html'...\033[2m"
	sed "s/{%API}/$API/g" $INPUTDIR/index.html > $OUTPUTDIR/index.html

	echo -e "\033[0m\033[1mBuilding '$API.html'...\033[2m"
	raml2html -i $OUTPUTDIR/$API.raml -o $OUTPUTDIR/$API.html

	echo -e "\033[0m\033[1mOpening '$API.html'...\033[2m"
	open $OUTPUTDIR/$API.html

	echo -e "\033[0m"
fi
