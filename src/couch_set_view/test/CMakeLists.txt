CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/run.tpl
               ${CMAKE_CURRENT_BINARY_DIR}/run)

FILE(GLOB TEST_FILES *.t)
LIST(SORT TEST_FILES)

FOREACH (it ${TEST_FILES})
   GET_FILENAME_COMPONENT(testname ${it} NAME_WE)
   ADD_TEST(couchdb-couch_set_view-${testname} ${PYTHON_EXECUTABLE} ${COUCHDB_RUNTEST} -c ${COUCHSTORE_BIN_PATH} -p ${COUCHDB_BIN_PATH}/src -m couch_set_view/test -t ${it} --verbose)
ENDFOREACH (it)

FILE(GLOB COUCH_SET_VIEW_TEST_SRC *.erl)
ERL_BUILD("couch_set_view_test" ${COUCH_SET_VIEW_TEST_SRC})
