ARG FROM_IMAGE=vnv_petsc
FROM ${FROM_IMAGE}:latest

ARG COMMIT_HASH=unknown
LABEL vnv.version.mfem=${COMMIT_HASH}

ENV MFEM_DIR=${SOFTWARE_DIR}/mfem

COPY . ${SOURCE_DIR}/mfem 

#Install MOOSE with VnV
RUN cd ${SOURCE_DIR}/mfem \
    && mkdir docker_build \
    && cd docker_build \
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
    && make install \
    && make examples

ENV VNV_CONFIG=${VNV_CONFIG}:${SOURCE_DIR}/mfem/docker_build/vnv.__registration__
ENV VNV_CONFIG=${VNV_CONFIG}:${SOURCE_DIR}/mfem/docker/config/vnv.__registration__








