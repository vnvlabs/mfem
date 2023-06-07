ARG FROM_IMAGE=vnv_petsc
FROM ${FROM_IMAGE}


ENV MFEM_DIR=${SOFTWARE_DIR}/mfem

COPY . ${SOURCE_DIR}/mfem 

#Install MOOSE with VnV
RUN cd ${SOURCE_DIR}/mfem \
    && mkdir build \
    && cd build \
    && cmake -DHYPRE_DIR=${HYPRE_DIR}\
             -DMETIS_DIR=${PETSC_DIR}\
             -DPETSC_DIR=${PETSC_DIR}\
             -DPETSC_ARCH=${PETSC_ARCH}\
             -DInjection_DIR=${VNV_DIR}/lib/cmake/\
             -DMFEM_USE_PETSC=ON\
             -DMFEM_USE_VNV=ON\
             -DCMAKE_EXPORT_COMPILE_COMMANDS=ON\
             -DBUILD_SHARED_LIBS=ON\
             -DCMAKE_INSTALL_PREFIX=${MFEM_DIR} .. \
    && make -j 8 \
    && make install 

#Build the examples 
RUN cd ${SOURCE_DIR}/mfem && cp -r vnv/examples ${MFEM_DIR}/examples && cd ${MFEM_DIR}/examples && mkdir build && cd build    

#Set up the vnv mfem customizations. 
RUN cp -r ${SOURCE_DIR}/mfem/vnv/gui ${MFEM_DIR}/gui 
ENV VNV_CONFIG=${VNV_CONFIG}:${SOFTWARE_DIR}/mfem/gui/vnv.__registration__ 

RUN rm -r ${SOURCE_DIR}/mfem 










