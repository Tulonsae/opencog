INCLUDE_DIRECTORIES(
    ${GUILE_INCLUDE_DIR}
)

ADD_LIBRARY (smob SHARED
	SchemeEval.cc
	SchemeExec.cc
	SchemePrimitive.cc
	SchemeSmob.cc
	SchemeSmobAtom.cc
	SchemeSmobAV.cc
	SchemeSmobGC.cc
	SchemeSmobNew.cc
	SchemeSmobTV.cc
	SchemeSmobVH.cc
	load-file
)

TARGET_LINK_LIBRARIES(smob
	${GUILE_LIBRARIES}
)

ADD_EXECUTABLE(PrimitiveExample
	PrimitiveExample.cc
)
TARGET_LINK_LIBRARIES(PrimitiveExample
	smob
	atomspace
	server
)

IF (WIN32)
    INSTALL (TARGETS smob DESTINATION "lib${LIB_DIR_SUFFIX}/opencog")
ENDIF (WIN32)

INSTALL (FILES
	SchemeEval.h
	SchemePrimitive.h
	SchemeSmob.h
	load-file.h
	DESTINATION "include/${PROJECT_NAME}/guile"
)
