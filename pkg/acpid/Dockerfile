FROM linuxkit/alpine:2e362f4459ba4491655061cccdd2fcc7a2de5eb3 AS mirror

RUN mkdir -p /out/etc/apk && cp -r /etc/apk/* /out/etc/apk/
RUN apk add --no-cache --initdb -p /out \
    alpine-baselayout \
    busybox
RUN rm -rf /out/etc/apk /out/lib/apk /out/var/cache

FROM linuxkit/alpine:2e362f4459ba4491655061cccdd2fcc7a2de5eb3 AS mirror2
RUN mkdir -p /out/etc/apk && cp -r /etc/apk/* /out/etc/apk/
RUN apk add --no-cache --initdb -p /out \
    busybox-initscripts
RUN rm -rf /out/etc/apk /out/lib/apk /out/var/cache

FROM scratch
COPY --from=mirror /out/ /
COPY --from=mirror2 /out/etc/acpi /etc/acpi

CMD ["/sbin/acpid", "-f", "-d"]

LABEL org.mobyproject.config='{"binds": ["/dev:/dev"], "pid": "host"}'

