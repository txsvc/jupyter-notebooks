FROM registry.access.redhat.com/ubi8/python-39:1-48

USER root

ENV JUPYTER_MAJOR_VERSION=1 \
    JUPYTER_MINOR_VERSION=16 \
    JUPYTER_PATCH_VERSION=12 \
    CONTAINER_NAME="jupyter-notebook"

ENV VERSION=$JUPYTER_MAJOR_VERSION.$JUPYTER_MINOR_VERSION.$JUPYTER_PATCH_VERSION \
    SUMMARY="Base image for building Jupyter notebooks" \
    DESCRIPTION="Base image for building Jupyter notebooks"
    
LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="Jupyter $VERSION" \
      io.openshift.tags="builder,python,jupyter${JUPYTER_MAJOR_VERSION}${JUPYTER_MINOR_VERSION}" \
      name="$CONTAINER_NAME" \
      version="$VERSION"

#io.openshift.s2i.scripts-url="image:///opt/app-root/builder"

# Copy the custom S2I scripts to $STI_SCRIPTS_PATH.
COPY ./s2i/bin/ $STI_SCRIPTS_PATH

RUN chown -R 1001:0 $STI_SCRIPTS_PATH && chown -R 1001:0 $APP_ROOT
USER 1001

# build using the custom script
RUN ls -la /tmp/src
RUN ./builder/assemble

# Set the default CMD to print the usage of the language image.
CMD $STI_SCRIPTS_PATH/usage